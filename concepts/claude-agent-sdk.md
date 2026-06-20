---
title: Claude Agent SDK (Unit 6)
tags: [claude, agent, sdk, multi-agent, tool-use, python, production]
category: concepts
created: 2026-06-14
updated: 2026-06-14
sources: [claude-complete-guide-2026]
summary: "Claude Agent SDK ครบ: Chatbot vs Agent, 5 Core Components, Multi-Agent Patterns, Safety/HITL, Production Observability, Memory Architecture, Error Handling พร้อม Python code 15 ตัวอย่าง"
provenance:
  extracted: 0.90
  inferred: 0.10
  ambiguous: 0.00
---

# Claude Agent SDK (Unit 6)

**Agent = Claude ที่ทำงานซ้ำในลูป, เรียก tools เอง, ตัดสินใจ next step เอง จนกว่าจะเสร็จ**

---

## 6.0 จาก Chatbot สู่ Agent — ความแตกต่างที่สำคัญ

| ด้าน | Chatbot | Agent |
|---|---|---|
| การทำงาน | รับ input → ตอบ output (ครั้งเดียว) | วางแผน → ทำ action → ประเมิน → loop |
| Decision making | Fixed responses | Claude ตัดสินใจ next action เอง |
| Tool use | Limited/none | เรียก tools, APIs, subagents |
| Duration | Single exchange | Minutes to hours |
| Error handling | Returns error | Retry + self-correct |
| Human oversight | Every turn | Checkpoints only |
| Example | Customer FAQ bot | "Research and write competitive analysis on X" |

**Key stats:** 5 Core Components · 3 Agent Roles · HITL requirement ใน production

---

## 6.1 Agent Architecture — 5 Core Components

| # | Component | ทำอะไร | ตัวอย่าง |
|---|---|---|---|
| 1 | **Perception** | รับ input จากทุก source | Text, files, tool results, user messages |
| 2 | **Memory** | เก็บ context | In-context + External KV + Vector + Episodic |
| 3 | **Planning** | วางแผนแยก subtasks | Chain-of-Thought, break goal into steps |
| 4 | **Action** | ทำ actions จริง | เรียก tools, เขียนไฟล์, เรียก subagents |
| 5 | **Self-evaluation** | ตรวจงานตัวเอง | Retry / adjust / continue / stop |

---

## 6.2 Claude Agent SDK Components

| Component | Role |
|---|---|
| Anthropic Client | Connection to Claude API |
| Messages API | Send/receive conversation turns |
| Tool definitions | JSON Schema ของ tools ที่ agent ใช้ |
| Tool execution | Code ที่ run tools จริง (you write this) |
| Streaming | Real-time response สำหรับ long tasks |
| Token counting | Monitor context usage |

### Basic Agent Loop

```python
def run_agent(task: str, tools: list, tool_functions: dict,
              max_iterations: int = 10) -> str:
    messages = [{'role': 'user', 'content': task}]
    for iteration in range(max_iterations):
        response = client.messages.create(
            model='claude-sonnet-4-6-20260101',
            max_tokens=4096,
            tools=tools,
            messages=messages)
        messages.append({'role': 'assistant', 'content': response.content})
        if response.stop_reason == 'end_turn':
            return response.content[0].text
        if response.stop_reason == 'tool_use':
            tool_results = []
            for block in response.content:
                if block.type == 'tool_use':
                    fn = tool_functions[block.name]
                    result = fn(**block.input)
                    tool_results.append({
                        'type': 'tool_result',
                        'tool_use_id': block.id,
                        'content': json.dumps(result)
                    })
            messages.append({'role': 'user', 'content': tool_results})
    return 'Max iterations reached'  # Safety limit
```

### Tool Definition JSON Schema

```python
tools = [
    {
        'name': 'search_web',
        'description': 'Search web. Returns [{title, url, snippet}].',
        'input_schema': {
            'type': 'object',
            'properties': {'query': {'type': 'string'}},
            'required': ['query']
        }
    },
    {
        'name': 'write_file',
        'description': 'Write content to a file.',
        'input_schema': {
            'type': 'object',
            'properties': {
                'path': {'type': 'string'},
                'content': {'type': 'string'}
            },
            'required': ['path', 'content']
        }
    }
]
```

**Best practice:** description ต้องชัดเจนว่า tool ทำอะไร + returns อะไร — Claude ใช้ description ตัดสินใจว่าจะเรียก tool ไหน

---

## 6.3 Multi-Agent Architecture

| Type | Description | ใช้เมื่อ |
|---|---|---|
| **Single Agent** | Agent เดียวทำทุก task | Simple tasks, prototype |
| **Orchestrator-Subagents** | Orchestrator plans, Subagents execute | Complex tasks, parallelism |
| **Peer-to-Peer** | Agents communicate directly | Collaborative, review tasks |
| **Hierarchical** | Multiple levels of orchestration | Enterprise-scale, mega tasks |

### Orchestrator Pattern

```python
def orchestrator_agent(goal: str) -> str:
    # Step 1: Plan with best model
    plan = client.messages.create(
        model='claude-opus-4-6-20260101',  # Best model for planning
        max_tokens=2048,
        messages=[{'role': 'user', 'content':
            f'Break this goal into 3-5 subtasks. Goal: {goal} '
            'Format: JSON list of {task, agent_type, priority}'}]
    ).content[0].text
    subtasks = json.loads(plan)
    # Step 2: Execute subtasks
    results = {}
    for subtask in subtasks:
        if subtask['agent_type'] == 'research':
            results[subtask['task']] = research_agent(subtask['task'])
        elif subtask['agent_type'] == 'write':
            results[subtask['task']] = writing_agent(subtask['task'])
    return synthesis_agent(goal, results)
```

### Specialized Subagents

```python
def research_agent(topic: str) -> str:
    system = 'You are a research specialist. Search web, find facts, cite sources.'
    return run_agent(f'Research: {topic}', search_tools, search_fns, system=system)

def writing_agent(brief: str) -> str:
    system = 'You are a writing specialist. Create clear, engaging content.'
    return run_agent(f'Write: {brief}', file_tools, file_fns, system=system)
```

---

## 6.4 Real-World Agent Patterns — 5 Production Patterns

> เลือกตาม use case ไม่ใช่ตาม 'coolness' — ทุก pattern มี tradeoffs ที่ชัดเจน

### 1. Research & Report Agent
Input: "Write competitive analysis report on [topic]"
1. Orchestrator breaks into research subtasks
2. Research Agent searches 5+ sources per topic
3. Analysis Agent extracts key insights
4. Writing Agent drafts sections in parallel
5. Review Agent fact-checks and edits
6. Orchestrator assembles final report

*Use cases: Market research, due diligence, academic research*

### 2. Code Review Pipeline
Input: PR diff → comprehensive review
1. Parser Agent reads PR diff and metadata
2. Security Agent scans for vulnerabilities
3. Performance Agent identifies bottlenecks
4. Style Agent checks coding standards
5. Test Agent verifies test coverage
6. Summary Agent writes review comment

*Use cases: Software development, DevOps, code quality*

### 3. Customer Support Escalation
Input: Complex customer issue
1. Triage Agent classifies issue type and urgency
2. Knowledge Agent searches internal docs/DB
3. Solution Agent generates response options
4. Quality Agent scores each option
5. Human confirms if high-stakes
6. Communication Agent formats final response

*Use cases: E-commerce, SaaS, financial services*

### 4. Data Processing Pipeline
Input: Process 10,000 documents
1. Batch Agent splits into chunks
2. N Extraction Agents run in parallel
3. Validation Agent checks each result
4. Aggregation Agent combines results
5. Report Agent creates summary

*Use cases: Legal, finance, healthcare, HR*

### 5. Content Production Pipeline
Input: Weekly content package
1. Strategy Agent plans week's content
2. Research Agent gathers trending topics
3. Writing Agents create 5 posts in parallel
4. SEO Agent optimizes each post
5. Social Agent creates platform versions
6. Scheduler Agent queues all content

*Use cases: Marketing agencies, content creators, brands*

---

## 6.5 Safety & Human-in-the-Loop — หลักการที่ไม่ควรข้าม

**Agent ที่ทำงานได้ = Agent ที่สามารถทำผิดพลาดได้เอง — HITL ไม่ใช่ optional สำหรับ production**

### Action Risk Levels (ตาราง 6.3)

| Action Type | ตัวอย่าง | HITL Requirement | ระดับความเสี่ยง |
|---|---|---|---|
| Read-only | ค้นหา web, อ่านไฟล์, query DB | ไม่จำเป็น | ต่ำ |
| Write (reversible) | Create files, draft documents | แนะนำ | ต่ำ–ปานกลาง |
| Write (hard to reverse) | Send email, post to social | จำเป็น | ปานกลาง |
| Delete/modify | ลบไฟล์, แก้ DB, cancel orders | จำเป็นมาก | สูง |
| Financial | Process payment, transfer funds | จำเป็นเสมอ | สูงมาก |
| Access control | Grant permissions, create users | จำเป็นเสมอ | สูงมาก |

### HumanCheckpoint Class

```python
class HumanCheckpoint:
    def __init__(self, auto_approve_low_risk: bool = False):
        self.auto_approve = auto_approve_low_risk

    def confirm(self, action: str, risk: str, details: dict) -> bool:
        if risk == 'LOW' and self.auto_approve:
            return True
        print(f'\n[AGENT ACTION REQUEST]')
        print(f'Action: {action}')
        print(f'Risk: {risk}')
        print(f'Details: {details}')
        response = input('Approve? (yes/no/modify): ').strip().lower()
        if response == 'modify':
            print('Current details:', details)
            for key in details:
                new_val = input(f' {key} [{details[key]}]: ').strip()
                if new_val: details[key] = new_val
        return response in ['yes', 'y', '']
```

### Minimal Footprint Principle

1. **Request only necessary permissions** — Agent ที่ต้อง read files ไม่ควรขอ write permissions — Principle of least privilege
2. **Prefer reversible over irreversible** — ถ้าทำได้สองวิธี เลือกวิธีที่ย้อนกลับได้ เช่น move to trash แทน permanent delete
3. **Confirm before high-impact actions** — ทุก action ที่ส่งผลภายนอก (email sent, payment processed) ต้องมี confirmation
4. **Explicit task scope** — บอก agent ว่าทำ task นี้เท่านั้น อย่าให้ scope กว้างจน agent ทำสิ่งที่ไม่ได้ตั้งใจ

### Prompt Injection ใน Agentic Context — อันตรายสูงกว่า Chatbot

> Agent ที่ browse web หรืออ่าน documents อาจเจอ 'invisible instructions' ที่ฝังใน content เพื่อ hijack agent
> ป้องกัน: validate all tool results, ไม่ follow instructions จาก external content, ใช้ XML tags แยก instructions จาก data อย่างชัดเจน

---

## 6.6 Advanced Patterns — Parallel & Long-Running Agents

### Pattern: Parallel Agent Execution

```python
import asyncio
import anthropic

async def async_subagent(client, task: str, system: str) -> str:
    response = await client.messages.create(
        model='claude-sonnet-4-6-20260101',
        max_tokens=2048,
        system=system,
        messages=[{'role': 'user', 'content': task}])
    return response.content[0].text

async def parallel_research(topics: list[str]) -> dict:
    client = anthropic.AsyncAnthropic()
    system = 'You are a research specialist. Return JSON with key facts.'
    tasks = [async_subagent(client, f'Research: {t}', system) for t in topics]
    results = await asyncio.gather(*tasks)  # All topics in parallel
    return dict(zip(topics, results))

# 5 topics: sequential = 50s, parallel = ~12s (4× faster)
results = asyncio.run(parallel_research(['Topic A', 'B', 'C', 'D', 'E']))
```

### Pattern: Long-Running Agent with Checkpointing

```python
import json, os
from dataclasses import dataclass, asdict

@dataclass
class AgentState:
    task_id: str
    goal: str
    completed_steps: list
    pending_steps: list
    results: dict
    status: str  # running/paused/completed/failed

def save_checkpoint(state: AgentState, path: str):
    with open(path, 'w') as f:
        json.dump(asdict(state), f)

def load_checkpoint(path: str) -> AgentState | None:
    if not os.path.exists(path):
        return None
    with open(path) as f:
        return AgentState(**json.load(f))

def resumable_agent(task_id: str, goal: str) -> str:
    checkpoint_path = f'checkpoints/{task_id}.json'
    state = load_checkpoint(checkpoint_path) or AgentState(
        task_id=task_id, goal=goal,
        completed_steps=[], pending_steps=plan_steps(goal),
        results={}, status='running')
    for step in state.pending_steps[:]:
        result = execute_step(step)
        state.completed_steps.append(step)
        state.pending_steps.remove(step)
        state.results[step] = result
        save_checkpoint(state, checkpoint_path)  # Save after each step
    state.status = 'completed'
    return synthesize(state.results)
```

---

## 6.7 Production Considerations (ตาราง 6.4)

| ด้าน | ความต้องการ | Implementation |
|---|---|---|
| Observability | Log ทุก action + decision | Structured logging + Sentry/Datadog |
| Rate limiting | ป้องกัน runaway agents | Max iterations + time budget |
| Cost control | ป้องกัน unexpected bills | Token budget per run, daily limits |
| Error recovery | Handle failures gracefully | Retry with backoff, fallback paths |
| Audit trail | รู้ว่า agent ทำอะไรไปแล้ว | Immutable action log in database |
| Testing | ทดสอบโดยไม่มี side effects | Sandbox mode, mock tools |
| Rollback | ย้อนกลับ actions ได้ | Snapshot before write, soft deletes |

### Agent Observability — Logging Decorator

```python
import logging, json
from datetime import datetime, timezone
from functools import wraps

logger = logging.getLogger('agent')

def log_action(action_type: str):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            start = datetime.now(timezone.utc)
            log_entry = {
                'action': action_type,
                'input': str(kwargs)[:200],
                'timestamp': start.isoformat()
            }
            try:
                result = func(*args, **kwargs)
                log_entry.update({
                    'status': 'success',
                    'duration_ms': int((datetime.now(timezone.utc)-start).total_seconds()*1000)
                })
                logger.info(json.dumps(log_entry))
                return result
            except Exception as e:
                log_entry.update({'status': 'error', 'error': str(e)})
                logger.error(json.dumps(log_entry))
                raise
        return wrapper
    return decorator

@log_action('web_search')
def search_web(query: str, num_results: int = 5): ...
```

### Cost Control — Token Budget Controller

```python
class TokenBudgetController:
    def __init__(self, max_tokens: int = 100_000, warn_at: float = 0.8):
        self.max_tokens = max_tokens
        self.warn_at = warn_at
        self.used_tokens = 0

    def check_budget(self, estimated_tokens: int) -> bool:
        '''Returns False if budget exceeded'''
        projected = self.used_tokens + estimated_tokens
        if projected > self.max_tokens:
            print(f'[BUDGET] Limit reached: {self.used_tokens}/{self.max_tokens}')
            return False
        if projected > self.max_tokens * self.warn_at:
            print(f'[BUDGET] Warning: {projected/self.max_tokens:.0%} used')
        return True

    def record_usage(self, response):
        self.used_tokens += response.usage.input_tokens
        self.used_tokens += response.usage.output_tokens
```

---

## 6.8 Testing Agents (ตาราง 6.5)

| Testing Layer | วัตถุประสงค์ | วิธีทำ | ความถี่ |
|---|---|---|---|
| Unit tests | ทดสอบ individual tools | Mock API calls, assert output | ทุก commit |
| Integration tests | ทดสอบ agent loop ทั้งหมด | Use sandbox tools (no side effects) | ทุก deploy |
| Scenario tests | ทดสอบ real-world scenarios | Run with test fixtures | Weekly |
| Adversarial tests | ทดสอบ injection + abuse | Intentional bad inputs | Monthly |
| Cost tests | verify ว่า token usage อยู่ใน range | Track tokens per scenario | ทุก deploy |

### Agent Test Harness

```python
class AgentTestHarness:
    def __init__(self, agent_fn, sandbox_tools: dict):
        self.agent = agent_fn
        self.tools = sandbox_tools  # Sandbox tools don't have real side effects
        self.action_log = []

    def run_test(self, task: str, expected_contains: list) -> dict:
        self.action_log = []
        result = self.agent(task, tool_functions=self.tools)
        passed = all(kw.lower() in result.lower() for kw in expected_contains)
        return {
            'task': task,
            'result': result,
            'passed': passed,
            'actions_taken': len(self.action_log),
            'tools_used': [a['tool'] for a in self.action_log]
        }

# Test cases
test_cases = [
    ('Research Python async patterns', ['async', 'await', 'asyncio']),
    ('Summarize the latest AI news', ['model', 'release', 'research']),
]
```

---

## 6.9 Claude เป็น Orchestrator — Directing Other AI Models

### Model Selection for Multi-Model Orchestration (ตาราง 6.6)

| Task Type | Model แนะนำ | เหตุผล | ราคาสัมพัทธ์ |
|---|---|---|---|
| Complex reasoning, strategy | Claude Opus | Best reasoning | สูง |
| General tasks, coding | Claude Sonnet | Balance speed/quality | ปานกลาง |
| Simple classification, fast | Claude Haiku | Fast + cheap | ต่ำ |
| Image generation | DALL-E / Flux | Claude ไม่ generate images | ตามใช้งาน |
| Speech-to-text | Whisper | Specialized for audio | ตามใช้งาน |
| Code execution | Claude Code + interpreter | Safe execution | ตาม compute |

### Smart Model Routing

```python
def smart_orchestrator(task: str) -> str:
    # Step 1: Haiku classifies (cheap + fast)
    task_type = haiku_client.messages.create(
        model='claude-haiku-4-5-20260101', max_tokens=50,
        messages=[{'role': 'user', 'content':
            f'Classify this task: {task}\n'
            'Categories: simple-qa | research | creative | code | analysis'}]
    ).content[0].text.strip()
    # Step 2: Route to appropriate model
    if 'analysis' in task_type or 'research' in task_type:
        model = 'claude-opus-4-6-20260101'
    elif 'code' in task_type:
        model = 'claude-sonnet-4-6-20260101'
    else:
        model = 'claude-haiku-4-5-20260101'
    return client.messages.create(
        model=model, max_tokens=4096,
        messages=[{'role': 'user', 'content': task}]
    ).content[0].text
```

### Model Selection Decision Tree

- **Task requires deep reasoning/complex analysis?** → Use Opus + Extended Thinking
- **Task involves lots of text generation (> 1,000 tokens)?** → Use Sonnet (best quality/price for generation)
- **Simple classification or short response (< 200 tokens)?** → Use Haiku (fastest + cheapest)
- **Default:** Sonnet

---

## 6.10 Complete Agent Examples

### Example 1: Research Agent (Complete)

```python
import anthropic, json
client = anthropic.Anthropic()

research_tools = [
    {'name': 'search_web',
     'description': 'Search web. Returns [{title,url,snippet}].',
     'input_schema': {'type': 'object',
         'properties': {'query': {'type': 'string'}}, 'required': ['query']}},
    {'name': 'save_result',
     'description': 'Save a research finding.',
     'input_schema': {'type': 'object',
         'properties': {'key': {'type': 'string'}, 'value': {'type': 'string'}},
         'required': ['key', 'value']}}
]

findings = {}
def save_result(key: str, value: str) -> dict:
    findings[key] = value; return {'saved': True}

def research_agent(topic: str) -> str:
    system = '''Research agent. Gather info on the given topic.
Use search_web to find information.
Use save_result to store key findings as you go.
When done, write a comprehensive summary.'''
    messages = [{'role': 'user', 'content': f'Research: {topic}'}]
    for _ in range(10):  # Max 10 iterations
        r = client.messages.create(model='claude-sonnet-4-6-20260101',
            max_tokens=2048, tools=research_tools,
            system=system, messages=messages)
        messages.append({'role': 'assistant', 'content': r.content})
        if r.stop_reason == 'end_turn': return r.content[0].text
        results = []
        for b in r.content:
            if b.type == 'tool_use':
                fn = {'search_web': search_web, 'save_result': save_result}[b.name]
                results.append({'type': 'tool_result',
                    'tool_use_id': b.id, 'content': json.dumps(fn(**b.input))})
        messages.append({'role': 'user', 'content': results})
    return 'Max iterations reached'
```

### Example 2: File Processing Agent

```python
import os, pathlib

file_tools = [
    {'name': 'list_files', 'description': 'List files in directory.',
     'input_schema': {'type': 'object',
         'properties': {'path': {'type': 'string'}}, 'required': ['path']}},
    {'name': 'read_file', 'description': 'Read file content.',
     'input_schema': {'type': 'object',
         'properties': {'path': {'type': 'string'}}, 'required': ['path']}},
    {'name': 'write_file', 'description': 'Write content to file.',
     'input_schema': {'type': 'object',
         'properties': {'path': {'type': 'string'}, 'content': {'type': 'string'}},
         'required': ['path', 'content']}}
]

def file_agent(instruction: str, working_dir: str) -> str:
    system = f'''File processing agent working in: {working_dir}
You can list, read, and write files in this directory only.
Complete the given task using the available tools.'''
    return run_agent(instruction, file_tools, file_fns, system=system)

# Example
result = file_agent(
    'Read all .txt files, create a summary.md with key points from each',
    working_dir='/tmp/documents')
```

---

## 6.12 Memory Architecture สำหรับ Long-running Agents

Memory คือสิ่งที่ให้ agent เรียนรู้จาก past experience และทำงาน tasks ที่ยาวกว่า context window ได้

| Memory Type | Storage | เข้าถึงอย่างไร | เหมาะกับ |
|---|---|---|---|
| In-context | Claude's context window | อ่านได้ทันที | Working memory: current task |
| External (KV) | Redis/DynamoDB | API call | Session state, user preferences |
| External (Vector) | Pinecone/Weaviate | Semantic search | Long-term knowledge, RAG |
| Episodic | Database | Query by time/task | Past actions, lessons learned |

### Hybrid Memory System

```python
from anthropic import Anthropic
import redis, json

class AgentMemory:
    def __init__(self, agent_id: str):
        self.agent_id = agent_id
        self.working = []  # In-context: last N messages
        self.kv = redis.Redis()  # Short-term: session state
        self.max_working = 20

    def add_message(self, role: str, content: str):
        self.working.append({'role': role, 'content': content})
        if len(self.working) > self.max_working:
            # Summarize oldest messages before trimming
            summary = self._summarize(self.working[:5])
            self.save_to_kv('summary', summary)
            self.working = self.working[5:]

    def save_to_kv(self, key: str, value: str):
        full_key = f'agent:{self.agent_id}:{key}'
        self.kv.setex(full_key, 3600, json.dumps(value))

    def get_context(self) -> str:
        '''Returns relevant past context to prepend'''
        summary = self.kv.get(f'agent:{self.agent_id}:summary')
        if summary:
            return f'Previous context summary: {json.loads(summary)}'
        return ''
```

---

## 6.13 Error Handling Patterns สำหรับ Agents (ตาราง 6.8)

| Error Type | สาเหตุ | Recovery Strategy |
|---|---|---|
| Tool failure | External API down | Retry 3x → fallback tool → notify |
| Invalid tool call | Wrong parameter types | Validate before execute → feedback to Claude |
| Infinite loop | Claude ไม่แน่ใจ next step | Detect repeated actions → interrupt + ask |
| Context overflow | Task ยาวเกิน context | Summarize + restart with summary |
| Wrong direction | Claude เข้าใจ goal ผิด | Checkpoint review → human correction |
| Resource exhaustion | Time/token budget exceeded | Graceful stop + partial result |

### Robust Tool Executor with Retry

```python
import time, random
from typing import Any

def execute_tool_safely(tool_name: str, tool_fn: callable,
                        inputs: dict, max_retries: int = 3) -> Any:
    last_error = None
    for attempt in range(max_retries):
        try:
            result = tool_fn(**inputs)
            return {'success': True, 'result': result}
        except ConnectionError as e:
            last_error = e
            wait = (2 ** attempt) + random.uniform(0, 1)
            print(f'Tool {tool_name} failed (attempt {attempt+1}). Waiting {wait:.1f}s')
            time.sleep(wait)
        except ValueError as e:
            # Input validation error - don't retry
            return {'success': False,
                'error': f'Invalid input: {e}',
                'should_retry': False}
        except Exception as e:
            last_error = e
    return {'success': False,
        'error': f'Tool failed after {max_retries} attempts: {last_error}',
        'should_retry': True}
```

---

## 6.14 Debugging Agents

Debug agent ยากกว่า debug code ธรรมดา เพราะพฤติกรรมมัน non-deterministic และ error อาจเกิดใน iteration ที่ 7 ของ loop ที่ 3

- **Verbose Mode — Print ทุก Step:** เพิ่ม print statement ใน agent loop เพื่อเห็นว่า Claude ตัดสินใจอะไร: current state, tool being called, tool result, Claude's reasoning
- **Replay Mode — บันทึกและ Replay:** บันทึก all tool call inputs/outputs ลง JSONL file เพื่อ replay conversation โดยใช้ cached tool results แทน real calls — เร็วกว่าและไม่เสีย token
- **Step-through Debugger:** หยุดก่อนทุก tool execution เพื่อ inspect ว่า Claude จะทำอะไร ให้ human approve/modify ก่อน execute เหมือน debugger แบบ step-over
- **Trace Visualization:** สร้าง Mermaid diagram จาก action log เพื่อ visualize flow ของ agent เห็น bottlenecks และ inefficiencies ได้ชัดเจน

---

## 6.15 Agent Use Case Gallery — ตัวอย่างจาก Industry จริง

| Industry | Agent | ROI |
|---|---|---|
| **FinTech** — Financial Report Agent | Collects 5 financial APIs → calculations + ratio analysis → PDF report with charts → email stakeholders → runs nightly | 8 hours manual → 15 minutes |
| **Healthcare** — Medical Literature Agent | Searches PubMed → extracts key findings → cross-references existing knowledge → structured summary for doctors → flags papers needing expert review | Literature review: 20 hours → 2 hours |
| **Legal** — Contract Review Agent | Reads contract PDF via Files API → identifies + categorizes all clauses → flags non-standard terms vs template → calculates risk score → outputs redline suggestions | First pass review: 3 hours → 20 minutes |
| **E-commerce** — Catalog Management Agent | Receives product data from supplier → generates SEO-optimized descriptions → creates platform-specific variants → uploads to 3 marketplaces → monitors + updates pricing | 100 products: 5 days → 2 hours |
| **HR** — Resume Screening Agent | Reads JD and requirements → processes each resume against criteria → scores and ranks candidates → generates interview questions per candidate → Human reviews top 10% only | 100 resumes: 8 hours → 30 minutes |

---

## 6.16 Common Mistakes ในการ Build Agents

1. **Build complex multi-agent ก่อนที่ single agent ทำงานได้** — เริ่มจาก single agent ทำ 1 task แล้ว verify ว่า work ก่อน เพิ่ม complexity ทีละชั้น — multi-agent ที่ build บน broken single agent = ยิ่งแย่
2. **ไม่มี max_iterations limit** — Agent ที่ไม่มี safety limit อาจวน loop จนค่า token ถึงหลักพัน ตั้ง max_iterations ทุกครั้งและ alert เมื่อใกล้ limit
3. **Tools มี description ไม่ชัดเจน** — Claude ตัดสินใจเรียก tool ไดโดยอ่าน description เป็นหลัก description ที่กว้าง = Claude เรียก tool ผิด — บอกชัดว่า: ทำอะไร รับ input อะไร return อะไร เมื่อไหร่ใช้
4. **ให้ Agent access กับ production data โดยตรง** — Agent ที่ทดสอบใน development แล้ว suddenly access production DB ทำ damage ได้มาก ใช้ sandbox environment เสมอในระหว่าง development
5. **ไม่มี audit trail สำหรับ actions** — เมื่อ agent ทำอะไรผิด คุณต้องรู้ว่าทำอะไรไปแล้วเพื่อ undo — log ทุก action: timestamp, tool, inputs, outputs, success/fail

### Quick Reference — Agent SDK Prompts

| Topic | Prompt |
|---|---|
| **Agent Planning** | 'Plan this task as steps for an agent: [goal]. Output JSON: [{step_name, description, tools_needed, dependencies}]' |
| **Tool Design** | 'Design tools for agent that does [task]. For each tool: name, description (when to use, input, output), input_schema JSON.' |
| **System Prompt** | 'Write system prompt for [specialist] subagent. Role, capabilities, constraints, output format, escalation conditions.' |
| **Error Recovery** | 'This agent got stuck: [describe situation]. What went wrong? How should it recover? What rule to add to prevent recurrence?' |
| **Test Cases** | 'Generate 10 test cases for an agent that does [task]: happy path (4), edge cases (3), adversarial (2), resource limits (1).' |
| **Debug Help** | 'Agent took these actions: [action log]. Goal: [X]. It seems stuck at [step]. What is the likely issue? How to fix?' |
| **Optimize** | 'This agent runs [N] iterations on average for [task]. How can I reduce iterations? What can be parallelized?' |
| **Multi-agent Design** | 'Design a multi-agent system for: [complex goal]. What agents needed? What does each do? How do they communicate?' |

---

## 6.17 Agent Design Guide — จาก Idea สู่ Architecture

เมื่อมี idea ที่ต้องการ automate ใช้ decision framework นี้ออกแบบ architecture ที่เหมาะสม ก่อนเขียน code บรรทัดแรก

| Q | คำถาม | YES | NO |
|---|---|---|---|
| Q1 | Task ต้องการ real-world actions (write files, call APIs, send messages)? | ต้องใช้ Agent พร้อม HITL สำหรับ destructive actions | อาจใช้ enhanced prompting + Chain-of-Thought แทน |
| Q2 | Task ยาวเกิน 1 context window (~200K tokens)? | ต้องมี Memory System + Checkpointing | Single agent loop เพียงพอ |
| Q3 | มี subtasks ที่ทำ parallel ได้และ independent? | ใช้ Parallel Agents + asyncio.gather() | Sequential single agent ง่ายกว่า |
| Q4 | แต่ละ subtask ต้องการ expertise ที่ต่างกันมาก? | ใช้ Specialized Subagents ด้วย dedicated system prompts | Single agent ที่มี broad system prompt |
| Q5 | Task มี regulatory / financial / safety implications? | ต้องมี mandatory HITL checkpoints ทุก critical action | Soft HITL สำหรับ anomalous situations |

---

## 6.18 Cost Optimization สำหรับ Agents (ตาราง 6.9)

Agents ใช้ token มากกว่า chatbot เพราะ loop หลายรอบ ถ้าไม่ optimize agent ที่รัน 100 ครั้ง/วัน อาจมีค่าใช้จ่าย $50-500/วันโดยไม่จำเป็น

| Optimization | วิธีทำ | ประหยัดได้ | ความยาก |
|---|---|---|---|
| Use Haiku for simple steps | ให้ Haiku classify/route, Sonnet สำหรับ complex | 50–80% ในบาง steps | ง่าย |
| Prompt Caching | Cache system prompt + knowledge base | 60–90% สำหรับ repeated context | ง่าย |
| Tool call reduction | ออกแบบ tools ให้ fetch มากขึ้นต่อ call | 20–40% ลด iterations | ปานกลาง |
| Parallel > Sequential | รัน independent tasks พร้อมกัน | เร็วขึ้น 3–5× (ไม่ลด cost แต่ลด time) | ปานกลาง |
| Early stopping | หยุดทันทีเมื่อ goal achieved | 10–30% | ง่าย |
| Context pruning | ลบ tool results เก่าที่ไม่จำเป็น | 20–40% context size | ยาก |

```python
def cost_optimized_agent(task: str, subtasks: list) -> str:
    results = {}
    for subtask in subtasks:
        # Use cheapest model that can handle the subtask
        if subtask['complexity'] == 'simple':  # classify/filter
            model = 'claude-haiku-4-5-20260101'
        elif subtask['complexity'] == 'medium':  # analysis, writing
            model = 'claude-sonnet-4-6-20260101'
        else:  # complex reasoning, strategy
            model = 'claude-opus-4-6-20260101'
        results[subtask['name']] = run_subtask(subtask, model)
    # Final synthesis with Sonnet (not Opus — save cost)
    return synthesize(task, results, model='claude-sonnet-4-6-20260101')
```

---

## 6.19 Agent vs No-Agent — เมื่อไหร่ไม่ควรสร้าง Agent

| สถานการณ์ | แนะนำ | เหตุผล |
|---|---|---|
| งานที่ทำครั้งเดียว | Manual + Claude chat | Setup overhead ไม่คุ้ม |
| Output ต้องการ human creativity | Enhanced prompting | Agent ไม่ได้ creative กว่า |
| Task ไม่ต้องการ real-world actions | RAG + Q&A | Agent เพิ่ม complexity โดยไม่จำเป็น |
| Latency สำคัญ (< 2 วินาที) | Direct API call | Agent loop ช้าเกินไป |
| Budget จำกัดมาก | Simple automation script | Agent ใช้ token มาก |
| Team ไม่มี ML/AI experience | No-code tools (Zapier/Make) | Debug agent ยาก |

> **Rule of Thumb:** ควร Build Agent เมื่อ Task ใช้เวลา 30+ นาทีถ้าทำมือ AND ทำ 3+ ครั้ง/สัปดาห์ + ต้องการ tool use หรือ real-world actions + มี multiple decision points ที่ต้องการ intelligence ไม่ใช่แค่ rules — ถ้าตอบ YES ทั้ง 3 = Agent คุ้มแน่นอน

---

## 6.20 Production Deployment Checklist

ก่อน deploy agent ใน production ตรวจสอบทุกข้อนี้:

| หมวด | รายการ |
|---|---|
| [Safety] | max_iterations limit ตั้งไว้และ test แล้ว |
| [Safety] | Human checkpoint สำหรับทุก destructive action |
| [Safety] | Prompt injection protection ใน tool inputs |
| [Observability] | Action logging บันทึก inputs/outputs ทุก tool |
| [Observability] | Token usage tracking และ budget alert |
| [Observability] | Error monitoring (Sentry หรือเทียบเท่า) |
| [Testing] | Unit tests สำหรับ individual tools |
| [Testing] | Integration test ด้วย sandbox tools |
| [Testing] | Adversarial test ด้วย injection attempts |
| [Cost] | Token budget per run ตั้งไว้ |
| [Cost] | Model routing optimize แล้ว |
| [Recovery] | Checkpoint mechanism สำหรับ long-running tasks |
| [Recovery] | Graceful error handling และ partial result output |

---

## 6.11 สรุปบทที่ 6 — Checklist

ก่อนดำเนินต่อ ตรวจสอบว่าเข้าใจสิ่งเหล่านี้แล้ว:

1. เข้าใจความต่างระหว่าง Chatbot และ Agent — decision making, duration, error handling
2. รู้ 5 components ของ Agent Architecture: Perception, Memory, Planning, Action, Evaluation
3. เขียน Basic Agent Loop ที่วนรับ tool results จนกว่า task จะเสร็จได้
4. รู้จัก Multi-Agent Architecture: Orchestrator, Subagent และ Peer-to-Peer
5. สร้าง Specialized Subagents ด้วย dedicated system prompt และ tools
6. เข้าใจ 5 Real-World Patterns: Research, Code Review, Support, Data, Content
7. Implement Human-in-the-Loop Checkpoints สำหรับ high-risk actions
8. รู้ Minimal Footprint Principle และ Prompt Injection risks ใน agents
9. ใช้ Parallel execution ด้วย asyncio เพื่อลด wall time
10. Implement Observability: action logging, token budget, checkpointing

---

## Related

- [[concepts/prompt-engineering]] — 6-component prompt ที่ใช้เป็น agent system prompt
- [[concepts/claude-9-features]] — Tool Use API, MCP, Extended Thinking ที่ agent ใช้
- [[concepts/claude-products]] — Claude Code เป็น agent ที่ใช้ tool use ทุก action
- [[skills/claude-mini-workflows]] — W13 Chatbot ก่อนมาเป็น Agent
- [[references/claude-api-cheatsheet]] — Model IDs และ SDK ที่ใช้ใน code ตัวอย่าง
