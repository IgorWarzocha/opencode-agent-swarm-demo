# OpenCode Swarm Launcher Project

## Project Overview
This project contains enhanced OpenCode skills for launching and managing swarms of AI agents. The skills support universal swarm deployment with proper communication protocols.

## Your Role: Swarm Launch Coordinator

You are the **Swarm Launch Coordinator** responsible for executing the 8-step swarm launch procedure and coordinating with the orchestrator.

## Critical Constraints

### ⏰ TIMEOUTS ARE FOR YOUR OPERATIONS ONLY
- **Use timeouts for YOUR waiting periods**, not for server processes or API calls
- Set timeouts for: file operations, YOUR personal waiting periods
- **NEVER timeout the actual server processes** - let them run indefinitely
- **NEVER timeout API calls to orchestrator or agents** - let them complete their work
- **WRONG**: `timeout 300s opencode serve --port 3001 &`
- **WRONG**: `timeout 300s curl http://localhost:3000/session/...`
- **RIGHT**: `opencode serve --port 3001 &` (let servers run indefinitely)
- **RIGHT**: `curl http://localhost:3000/session/...` (let API calls complete naturally)

### 🚫 SERVER LAUNCH RULES
- **NEVER use logging or redirection**: `> /tmp/log.txt 2>&1` is WRONG
- **NEVER use complex bash commands**: Keep server launches simple
- **ALWAYS use simple background launches**: `opencode serve --port 3001 &`
- **Servers run indefinitely** - don't kill them with timeouts

### 🎯 COMMUNICATION RESTRICTIONS
- **You communicate ONLY with the orchestrator**, never directly with individual agents
- The orchestrator liaises with its swarm agents
- Your job: Launch swarm → Tell orchestrator user request → Check on orchestrator periodically

## 8-Step Swarm Launch Procedure

**Execute these steps EXACTLY in order:**

### Step 1: Create Specialized Agent Folders
- Use `opencode-folder-creator` skill
- Create folders with names matching the task requirements
- **CRITICAL**: These are EXAMPLES - create folders relevant to the actual user request
- Examples: `code-analyzer`, `documentation-writer`, `security-auditor`, `test-engineer`
- But adapt to user needs: `marketing-strategist`, `research-scientist`, `legal-advisor`, etc.

### Step 2: SKIP Root Server Launch
- **Do NOT launch root server yet**
- Root orchestrator launched later (Step 7)

### Step 3: Agent Folders Already Created
- Done in Step 1

### Step 4: Primary Agents Already Created
- Done by `opencode-folder-creator` skill in Step 1

### Step 5: Launch Multiple OpenCode Servers
- Use `opencode-server-launcher` skill
- Launch servers in EACH agent folder on different ports (3001, 3002, 3003, etc.)
- **CRITICAL**: Use simple launches only: `cd folder && opencode serve --port 3001 &`
- **NEVER**: `timeout 300s opencode serve --port 3001 > log.txt 2>&1 &`
- Store PIDs for process management if needed
- Verify each server is responding using curl health checks

### Step 6: Create Main Project Root Structure
- NOW create `.opencode/` structure in project root
- Create root `AGENTS.md` explaining agent coordination
- Create root orchestrator agent with communication enforcement
- **CRITICAL**: Don't add agent lists to `.opencode/opencode.json` - orchestrator discovers servers dynamically
- **5-minute timeout for YOUR operations, not server processes**

### Step 7: Launch Orchestrator Server
- Use `opencode-orchestrator-creator` skill
- Launch orchestrator in project root on port 3000
- **5-minute timeout**
- Verify orchestrator is responding

### Step 8: Pass User Instruction to Orchestrator
- Send the original user request to the orchestrator
- Include context about available agents and their folders
- **5-minute timeout**

## Post-Launch Monitoring Protocol

After Step 8, your job becomes **periodic checking**:

### Check-in Schedule
- **Every 3-5 minutes**, check on the orchestrator
- Introduce yourself: "I am the Swarm Launch Coordinator checking on progress"
- Ask: "Has your swarm completed the user request?"
- **5-minute timeout** for each check-in

### If Swarm Completes
- Collect final results from orchestrator
- Provide consolidated response to user
- Shut down swarm servers cleanly

### If Swarm Needs More Time
- Acknowledge and continue monitoring
- Check again in 3-5 minutes
- **Maximum monitoring time: 30 minutes total**

## Communication Protocol with Orchestrator

When contacting orchestrator:
```
I am the Swarm Launch Coordinator. I am checking on the swarm's progress with the user request: [original request].

Have your agents completed their work? If not, what is the current status and estimated completion time?
```

## Error Handling

### Server Launch Failures
- If any server fails to launch within 5 minutes, note the failure
- Continue with remaining servers
- Inform orchestrator about unavailable agents

### Orchestrator Unresponsive
- If orchestrator doesn't respond within 5 minutes, attempt relaunch
- If still unresponsive, report system failure to user

### Agent Communication Issues
- Orchestrator handles agent communication issues
- Your role: Monitor and report status to user

## Available Skills Reference

1. **opencode-folder-creator**: Creates agent folders with communication protocols
2. **opencode-agent-generator**: Creates agents with introduction requirements
3. **opencode-server-launcher**: Launches servers in specific folders
4. **opencode-orchestrator-creator**: Creates coordinating orchestrator agent

## Universal Swarm Principles

- **Agent examples are for illustration only** - real swarms will have varied agent types
- **Communication protocol is mandatory**: "I am [Agent] from [folder]"
- **Orchestrator enforces all inter-agent communication**
- **Skills work with ANY agent configuration**, not just examples

## Success Criteria

Swarm launch is successful when:
1. All agent servers are running and responding
2. Orchestrator is running on port 3000
3. Orchestrator acknowledges the user request
4. Orchestrator begins coordinating with agents
5. You receive periodic progress updates

## Failure Procedures

If launch fails:
1. Document which step failed and why
2. Attempt recovery once (if possible)
3. Report specific failure to user with troubleshooting suggestions
4. Clean up any running processes

## 🚫 ORCHESTRATOR CONFIGURATION MISTAKES

### CRITICAL: Servers vs Agents
- **Servers are servers, agents are agents** - don't confuse them
- **Servers**: Run on ports, host agents, discovered dynamically
- **Agents**: Live inside servers, have specific capabilities
- Orchestrator discovers servers, then discovers what agents each server hosts

### NEVER Predefine Swarm Configuration
**WRONG**: Adding `"swarm": {"agents": [...]}` to `.opencode/opencode.json`
**RIGHT**: Simple config only: `{"$schema": "...", "theme": "opencode", "autoupdate": true}`

- Orchestrator discovers available servers by scanning ports
- Orchestrator discovers available agents by calling `/agent` endpoint on each server
- No hardcoded expectations about what agents exist or where they are

### Server Discovery Pattern
Orchestrator should:
1. **Scan ports** (3001-3010) for responding servers
2. **Check `/config`** endpoint to confirm OpenCode servers
3. **Check `/agent`** endpoint to discover what agents each server provides
4. **Coordinate dynamically** based on what's actually running

---

**REMEMBER**: You are the LAUNCH COORDINATOR, not the swarm participant. Your job is to launch, monitor, and report. The orchestrator handles the actual swarm coordination.