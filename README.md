# From User Feedback to Governed Self-Improvement: The AIAUF Framework for Traceable Adaptation in Agentic AI Systems

**Jia-fan Sun¹, Meng Liu², Li-li Qiao³, Meng-na Zhou⁴, and Xing Yi⁵***

¹ Faculty of Accountancy and Management, Universiti Tunku Abdul Rahman, 43000 Kajang, Malaysia  
² School of Artificial Intelligence, Henan University, 450046 Zhengzhou, China  
³ Fudan Development Institute, Fudan University, 200433 Shanghai, China  
⁴ Zhaoxia Test Paper Research Institute (Luoyang) Co., Ltd., Kaiyuan Avenue, Luolong District, Luoyang, China  
⁵ Department of Educational Psychology and Counselling, Faculty of Education, Universiti Malaya, 50603 WPKL, Kuala Lumpur, Malaysia

sunjiafan521@gmail.com, mengliuedu@163.com, qiaolilia@outlook.com, 15029290268@163.com, freeyi1127@gmail.com

*\* Corresponding Author*

---

## Abstract

This article develops the AI Agents Self-Improvement with User Feedback framework (AIAUF) to explain how user experience can be converted into controlled improvement of agentic AI systems. Existing studies separately discuss agent loops, self-evolving agents, AI interviewing, MCP-based tool access, and spec-driven coding, but they rarely connect these elements into a governed feedback-to-implementation process. AIAUF addresses this gap by treating user feedback as research evidence rather than an automatic command for system change.

The framework contains five connected layers: adaptive AI interviewing for collecting contextual user experience; feedback distillation for cleaning, coding, clustering, and prioritizing responses; technical integration through MCP, Skills, memory, databases, repositories, and tools; controlled self-improvement through specification-based coding and verification; and governance for deciding whether a proposed change should be released, personalized, further tested, deferred, or rejected.

The article contributes a theoretical model linking human-centered AI, agentic architecture, and feedback-driven self-improvement. It also contributes a methodological design for scalable AI interviewing, a technical architecture for connecting qualitative evidence with implementation contexts, and a governance perspective that emphasizes traceability, validation, safety, and post-release evaluation. As a framework and design proposal, it defines mechanisms and evaluation criteria rather than reporting production performance. By organizing the path from conversational feedback to tested agent modification, AIAUF offers a structured basis for future prototypes, case studies, and comparative evaluation against conventional feedback pipelines.

**Keywords:** Agentic AI; AI agents; user feedback; AI interviewing; feedback distillation; Model Context Protocol; spec coding; AI governance

---

## 1. Introduction

Agentic AI is increasingly moving from single-turn response generation toward systems that can plan, use tools, remember prior interactions, and execute tasks across multiple steps. In this sense, agentic AI differs from ordinary chatbot interaction because the model is embedded in an operational loop involving perception, planning, action, observation, and result integration (Sapkota et al., 2025; Yao et al., 2022). Recent work on managed agents further separates the model, execution environment, and session record, which makes longer-horizon task execution more feasible (Lance et al., 2026). This shift is related to a broader movement from cooperative intelligence to more autonomous forms of intelligence. Cooperative intelligence emphasizes collaboration between humans and AI, while autonomous intelligence assigns more independent responsibility to AI systems (Jiang et al., 2024).

However, greater autonomy does not reduce the need for human-centered design. On the contrary, when agents begin to act on behalf of users, their improvement mechanisms should remain connected to user experience, user expectations, and accountable evaluation. At present, many AI agents can improve through prompt revision, memory updates, tool selection, workflow redesign, or iterative testing. Studies on self-evolving agents show that improvement does not always require model retraining — it can also occur at the system level, where agents adjust future behavior through feedback, memory, and optimization mechanisms (Fang et al., 2025; He et al., 2026; Zhuang et al., 2026). These developments create a practical question: how can user feedback become a structured signal for improving AI agents and software systems, without allowing raw feedback to directly trigger uncontrolled changes?

### 1.1 Problem Statement

The **first problem** is that many software and AI product improvement processes remain provider-centered. Users may report problems through surveys, support tickets, app reviews, public posts, or online communities, but the decision to interpret, prioritize, and implement those suggestions usually remains centralized. This mechanism is necessary for safety and consistency, yet it can delay responses to emerging user needs. For mass-market applications, the distance between user experience and product improvement can become especially large.

The **second problem** is that user feedback is difficult to process at scale. A small number of interviews can provide rich contextual insight, but they are costly and difficult to repeat across large and diverse user groups. Surveys can reach more users, but they often compress experience into predefined items and may miss unexpected needs. AI interviewing offers a possible middle path. Anthropic's large-scale AI interviewer study suggests that adaptive interviews can be conducted across many users, countries, and languages (Anthropic, 2025). Nevertheless, scale alone does not solve the problem of interpretation. Thousands of responses may contain repeated complaints, contradictory preferences, rare but serious problems, and suggestions that are attractive but technically or ethically unsuitable.

The **third problem** concerns the quality of AI interviewing. Existing studies show that AI interviewers can produce useful qualitative data, but they also have limitations. Wong et al. (2025) found that AI interviewers may skip topics, move too quickly, or introduce examples before participants have fully answered. Wuttke et al. (2025) found that GPT-based interviews can produce data broadly comparable to human interviews, but AI interviewers may be weaker at asking strong follow-up questions when answers are surprising or unclear. These findings suggest that AI interviewing should not be treated as a simple replacement for human interviewing. It requires interview protocols, stopping rules, quality checks, and validation.

The **fourth problem** is implementation control. Even if useful feedback is collected, it should not move directly into code, prompts, memory, or agent behavior. Vibe coding can accelerate development, but it is vulnerable to scope expansion, weak verification, hallucinated implementation details, and premature claims of success (Daniel, 2026; Meske et al., 2025). For feedback-driven improvement, user comments must be transformed into traceable requirements, then into specifications, tests, and governed updates. Spec coding provides one possible discipline for this process because it requires structured specifications before implementation (Marri, 2026).

The existing literature addresses important parts of this problem, but these parts are often studied separately. Agentic AI research explains how models can be organized into loops of reasoning, memory, tool use, and action (Sapkota et al., 2025; Yao et al., 2022). Self-improvement research explains how agents can revise prompts, workflows, memories, and strategies through iterative feedback (Fang et al., 2025; He et al., 2026; Zhuang et al., 2026). AI interviewing studies show that conversational systems can collect qualitative data at larger scale, while also facing limitations in probing, participant experience, reliability, and validation (Anthropic, 2025; Wong et al., 2025; Wuttke et al., 2025). Technical infrastructure such as MCP, Skills, memory, and spec coding shows how AI reasoning can be connected to external tools and controlled implementation environments (Anthropic, 2026; Balis et al., 2026; Marri, 2026). The gap is the lack of an integrated framework that connects these elements into a complete feedback-to-improvement loop.

### 1.2 Research Aim and Research Questions

The aim of this study is to design a governed framework through which AI agents can improve by collecting, distilling, structuring, and implementing user feedback under verification and evaluation constraints.

The central research question is:

> **How can an AI agent self-improvement framework transform user feedback into governed, traceable, and testable improvements?**

This question is divided into four specific research questions:

- **RQ1:** How can AI interviewing be designed to collect authentic, contextual, and actionable user experience at scale?
- **RQ2:** Which methodologies effectively distill raw user feedback into structured requirements while preserving traceability to the original evidence?
- **RQ3:** How can feedback-derived requirements relate to technical context, tools, memory, and repositories for controlled agent improvement?
- **RQ4:** How can spec coding, verification, and governance reduce the risk of uncontrolled or unsuitable updates in a feedback-driven self-improvement loop?

### 1.3 Proposed AIAUF Framework and Its Contributions

AIAUF is designed as a governed feedback-to-improvement framework. It does not assume that user comments should directly trigger system updates. Instead, it treats user feedback as a research signal that must be collected, interpreted, connected to technical context, specified, implemented, and evaluated. The framework contains five connected layers:

1. **AI Interviewing Module** — collects adaptive qualitative feedback from users
2. **Feedback Distillation Layer** — AI research agents clean, code, cluster, and prioritize user responses
3. **Technical Integration Layer** — MCP, Skills, memory, databases, and tools connect user requirements with product and implementation context
4. **Controlled Self-Improvement Layer** — spec coding translates approved requirements into implementation plans, tests, and updates
5. **Evaluation and Governance** — determines whether an improvement should be released globally, personalized, simulated further, or rejected

This study makes four contributions. First, it contributes a theoretical framework that links human-centered AI, agentic AI, and feedback-driven self-improvement. Second, it contributes a methodological design for using AI interviewing as a scalable but governed method for collecting user experience. Third, it contributes a technical architecture that connects feedback distillation, MCP-based context access, Skills, memory, and spec coding. Fourth, it contributes a governance-oriented view of agent self-improvement, where user feedback is valuable but must be filtered, validated, specified, and evaluated before it changes agent behavior.

---

## 2. Related Works

We reviewed the literature needed to support AIAUF. The review follows the logic of the framework rather than a general history of artificial intelligence. It first defines agentic AI as an execution system with memory, tools, and iterative action. It then reviews self-improvement in agentic systems, user feedback as an improvement signal, AI-supported social research, feedback distillation, MCP-based infrastructure, and spec coding.

### 2.1 Foundations of Agentic AI

Agentic AI refers to an execution-oriented form of large language model application in which the model is embedded in a loop of perception, planning, tool use, observation, and result integration. It is different from a single-turn question-answering system because the user request is translated into operational intent, decomposed into subtasks, routed to tools or skills, and recombined into an accountable response (Sapkota et al., 2025). Claude Managed Agents further clarify this distinction by separating the model, the execution environment, and the durable session record. This separation supports longer-horizon work, recovery from failure, and safer handling of external resources (Lance et al., 2026).

Agentic AI also combines different architectural traditions, as summarized in Table 2.1.

**Table 2.1. Dual paradigm classification of agentic AI architectures**

| Dimension | Symbolic / Classical Paradigm | Neural / Generative Paradigm | Relevance to AIAUF |
|---|---|---|---|
| Core mechanism | Deterministic planning over explicit state | Prompt-guided language generation | AIAUF needs structured control and adaptive conversation |
| Memory model | Rule bases, graphs, or typed records | Session history and retrieved context | User feedback must become auditable memory |
| Reasoning style | Deductive and rule-based | Probabilistic and context-sensitive | Feedback interpretation needs judgement, but updates need constraints |
| Data modalities | Mainly structured data | Text, code, tables, images, and dialogue | User feedback mixes stories, preferences, and requirements |
| Methodological role | Automates formal pipelines | Bridges qualitative and quantitative work | AIAUF links interviewing, analysis, and implementation |
| Representative systems | SOAR, BDI agents, classical planners | ReAct, AutoGen, LangGraph | Agent loops support adaptive interviewing and improvement |

### 2.2 Self-Improvement in Agentic AI Systems

Studies of agentic AI self-improvement show that adaptation is not limited to model retraining. In deployed agents, improvement can occur through prompts, memory, tool use, workflow structure, execution strategy, and feedback interpretation. Fang et al. (2025) describe self-evolving agents as systems that act in an environment and use optimizers to adjust future behavior. Several mechanisms are already visible in recent work:

- **Test-Time Recursive Thinking** improves task performance by generating candidate solutions, comparing outcomes, and storing compact lessons for later use (Zhuang et al., 2026).
- **EvoTest** separates task execution from later adaptation, so an actor completes an episode while an evolver revises prompts, memories, tools, and decision parameters before the next episode (He et al., 2026).
- **SEW** applies similar logic to multi-agent coding workflows by evolving both workflow structure and agent prompts (S. Liu et al., 2026).

Self-improvement also creates risks. Shao et al. (2026) describe misevaluation, where memory accumulation, tool creation, model updates, or workflow changes can gradually shift an agent away from its original constraints. AIAUF therefore treats feedback as input to a governed improvement process, not as a direct command to update production behavior.

### 2.3 User Feedback as an Improvement Signal

The proposed framework begins with a shift from provider-centered update mechanisms to user-centered improvement. In conventional software development, feedback often passes through complaints, tickets, public posts, surveys, product meetings, and release approval. These channels can identify important issues, but they are usually slow and selective.

High-value feedback may reveal repeated breakdowns, unmet niche requirements, safety concerns, or user mental models that differ from provider assumptions. Raw conversation should not be passed directly to implementation — it should first be grounded, coded, structured, and checked.

### 2.4 AI-Supported Social Research for User Feedback Collection

The first research question draws on the long distinction between surveys and interviews. Surveys collect standardized data from large samples and support analysis of constructs such as trust, acceptance, risk, usefulness, and satisfaction. Interviews collect richer accounts of context, surprise, frustration, and expectation.

Recent studies suggest that AI interviewing can reduce the depth-scale tradeoff, but do not remove methodological risk. Anthropic's AI interviewer conducted approximately 81,000 adaptive interviews across many countries and languages, showing that conversational data collection can be scaled in ways difficult for human interview teams (Anthropic, 2025). Smaller empirical studies are more cautious: Wong et al. (2025) found that an AI interviewer for alternative protein research was useful but sometimes skipped topics or moved too quickly, while Wuttke et al. (2025) found that GPT-based interviews were weaker at asking for strong follow-ups when answers were surprising.

**Table 2.2. Traditional surveys and AI-powered interviews**

| Dimension | Traditional Surveys | AI-Powered Interviews | Implication for AIAUF |
|---|---|---|---|
| Question structure | Fixed questions and response options | Adaptive follow-ups based on prior answers | AI can probe unclear or surprising feedback |
| Scale | Often hundreds to several thousand participants | Potentially much larger samples when governed well | Large feedback pools become feasible |
| Data type | Mainly structured quantitative data | Qualitative narratives plus metadata | Distillation is required before implementation |
| Depth | Limited by predefined items | Can capture stories, examples, emotions, and edge cases | Useful for discovering unmet requirements |
| Risk | Item ambiguity and common method bias | Prompt bias, inconsistent probing, latency, and fatigue | Validation must be built into the workflow |

### 2.5 Agent Loop Architecture in AI Interviewing

AI interviewing depends on an agent loop because the interviewer must listen, update context, decide whether to probe, and decide when to stop. ReAct formalized a pattern in which reasoning traces are interleaved with actions and observations (Yao et al., 2022). An AI interviewer should be able to refine a follow-up question in light of previous answers rather than simply advance through a fixed script.

**Table 2.3. Mapping of queryLoop engineering properties onto qualitative interview protocol functions**

| queryLoop Property | Human Interview Analogue | Methodological Implication |
|---|---|---|
| Loop continues until an explicit terminal condition | Interviewer decides closure through substantive completion | Termination is condition-based, not only sequence-based |
| State messages carry conversation history | Interviewer's working memory | Follow-ups can use earlier answers |
| Transition records why the loop continued | Interviewer's probing rationale | Continuation logic becomes machine-readable |
| Async generator yields events turn by turn | Real-time interviewer response | Monitoring and intervention become possible |
| Tool use summaries record external actions | Field notes about instruments and sources | Tool-mediated steps become auditable |

*Adapted from Lin (2026, Ch. 3)*

### 2.6 From Raw Feedback to Structured Requirements

Collecting feedback is not enough. AIAUF requires a distillation layer that converts many raw interviews into structured, production-ready proposals. The layer should identify recurring problems, rare but consequential edge cases, contradictions across user groups, and requirements that can be translated into tests.

Recent AI survey studies show why checks are needed. Terry et al. (2025) found that ChatGPT-generated grit scale items had high internal reliability but mixed convergent validity. Khojasteh et al. (2025) developed the AI and Academic Writing Questionnaire and reported strong overall psychometric results while noting subscales with weak convergent validity. For AIAUF, the distillation model should therefore preserve traceability from requirement to source feedback. The goal is not to make qualitative feedback purely quantitative — it is to avoid treating raw conversation as implementation-ready before it has been interpreted and reviewed.

### 2.7 Technical Infrastructure: MCP, Skills, Memory, and Tools

A feedback-driven self-improvement framework requires infrastructure that connects models with data sources, tools, repositories, and execution environments. The Model Context Protocol standardizes how AI applications connect to external tools and data sources (Anthropic, 2026). MCP is relevant because AIAUF crosses several system boundaries: interview data may be stored in a database, the distillation agent may need access to coding taxonomies and product telemetry, and a spec coding agent may need repository access and test commands.

Skills provide another layer of structure. In AIAUF, a feedback-analysis Skill can define how to code user pain points, a product-requirement Skill can distinguish a request from a bug report, and a safety Skill can define what feedback cannot be implemented directly.

### 2.8 Spec Coding as Controlled Implementation of User Feedback

Vibe coding describes a practice in which developers state goals in natural language and LLMs generate implementation code. It can reduce barriers and speed up delivery, but it is vulnerable to hallucination, output drift, weak context retention, and limited verification (Meske et al., 2025). Daniel (2026) gives a practical critique: agents may add fields nobody requested, rename functions according to their own conventions, expand scope, or report success when the code compiles rather than when requirements are satisfied.

Spec coding responds by requiring a structured and verifiable specification before implementation. Marri (2026) presents spec coding as an engineering enhancement of vibe coding, where the system first establishes a specification, then generates code in staged iterations, and then uses tests and analysis for validation. In AIAUF, spec coding is the bridge between user feedback and controlled self-improvement.

### 2.9 Literature Gap and Positioning of the AIAUF Framework

The remaining gap is integration. Existing agent self-improvement studies often emphasize task performance or benchmark improvement rather than authentic user feedback. Existing AI interviewing studies often emphasize data collection rather than downstream product improvement. Existing spec coding discussions emphasize implementation control but usually do not begin with large-scale qualitative user research.

AIAUF is positioned at this intersection. It treats user feedback as the starting signal, AI interviewing as the collection method, distillation as the interpretive bridge, MCP as the integration infrastructure, and spec coding as the controlled implementation mechanism. Agentic AI provides the operational loop, social research provides the feedback method, psychometrics and qualitative validation provide robustness concerns, MCP provides tool access, and spec coding provides implementation discipline.

---

## 3. Structural Architecture of AIAUF

Based on the literature reviewed above, this study proposes the AI Agents Self-Improvement with User Feedback framework (AIAUF). The framework is designed to explain how user feedback can move from conversational evidence to controlled agent improvement. It does not assume that user comments should directly trigger system updates. Instead, AIAUF treats feedback as a research signal that must be collected, interpreted, connected to technical context, converted into specifications, and verified before implementation.

### 3.1 Overall Architecture of the AIAUF Feedback-to-Improvement Loop

AIAUF contains five connected layers: feedback collection, feedback distillation, technical integration, controlled implementation, and evaluation. The framework is recursive rather than linear — after an improvement is released or simulated, the system can collect new user feedback and compare it with earlier requirements. This loop supports continuous adaptation, but the loop is constrained by traceability, review, testing, and governance.

**Table 3.1. Main structural architecture of the AIAUF framework**

| Layer | Main Components | Input | Output | Control Point |
|---|---|---|---|---|
| Feedback collection | AI interviewer, interview script, conversation state | User experience and open-ended answers | Interview transcript and issue signals | Consent, probing quality, stopping rule |
| Feedback distillation | AI research agent, skills, memory | Raw transcripts and user metadata | Themes, requirements, priorities, evidence links | Reliability check, contradiction check, source trace |
| Integration | MCP, tools, database, repository access | Structured requirements and technical context | Retrieved code, product documents, test context | Permission, logging, context minimization |
| Spec coding | Coding agent, specification, planning, tests | Approved requirement | Implementation plan, code change, test result | Spec review, test execution, verification |
| Governance and evaluation | Human review, policy rules, release decision | Verified change and risk report | Release, personalization, rejection, or further study | Accountability, safety, post-release feedback |

### 3.2 User Feedback Collection Layer: AI Interviewing Module

The first layer is the AI Interviewing Module. Its task is to collect user experience at scale while preserving the depth normally associated with qualitative interviews. In AIAUF, the AI interviewer has four responsibilities:

1. Introduce the interview topic and obtain usable consent according to the research setting
2. Ask open questions about the user's experience with the agent or application
3. Produce follow-up questions when the answer is vague, surprising, contradictory, or related to a high-value issue
4. Stop the interview when enough information has been collected, not merely when a fixed number of questions has been reached

**Code Listing 3.1. Simplified interview loop in AIAUF**

```typescript
type InterviewState = {
  messages: Message[];
  userProfile?: UserProfile;
  unresolvedIssues: Issue[];
  transition?: "probe" | "clarify" | "close";
};

while (!shouldClose(state)) {
  const question = generateQuestion(state);
  const answer = await collectUserAnswer(question);
  state.messages.push(answer);
  state.unresolvedIssues = updateIssues(state.messages);
  state.transition = decideNextStep(state);
}
```

This code listing summarizes the architectural logic. The interviewer keeps conversation history, updates the current understanding of the user's problem, and decides whether to probe, clarify, or close. The module must also control known weaknesses of AI interviewing — the system may flag interviews with short answers, missing demographic context, or unresolved complaints for human review or a second interview round.

### 3.3 Feedback Distillation Layer: AI Research Agent, Skills, and Memory

The second layer is the feedback distillation layer. Raw interview transcripts are not implementation-ready. The AI Research Agent performs five analytic tasks:

1. Clean and segment interview transcripts
2. Identify recurring themes, edge cases, and minority needs
3. Distinguish different types of feedback (bug reports, usability problems, missing features, safety concerns, personalization requests)
4. Link each requirement to evidence from the original feedback
5. Rank requirements by frequency, severity, feasibility, and strategic relevance

**Code Listing 3.2. A concise requirement object for feedback distillation**

```json
{
  "requirement_id": "REQ-023",
  "theme": "follow-up question quality",
  "source_feedback": ["INT-102", "INT-188", "INT-245"],
  "user_problem": "AI interviewer ends too early when users give unclear answers",
  "proposed_change": "Add clarification trigger for vague or incomplete responses",
  "risk_level": "medium",
  "review_status": "pending"
}
```

This structure supports traceability. A coding agent can see the proposed change, but it also sees the evidence, risk level, and review status. This reduces the chance that conversational feedback becomes uncontrolled modification.

### 3.4 Integration Layer: MCP, Tools, Database, and Context Management

The third layer connects the research output with the technical environment. AIAUF requires access to feedback databases, product documents, code repositories, issue trackers, test suites, release notes, telemetry, and policy documents. Through MCP or equivalent tool protocols, agents can retrieve interview summaries, inspect product context, open related code files, run tests, and write structured implementation plans.

Context management is a key design issue. The system should not pass all available data into every agent call. The integration layer should therefore include permission control, logging, and data minimization. These controls are not secondary — they determine whether feedback-driven improvement remains accountable.

### 3.5 Controlled Self-Improvement Layer: AI Spec Coding, Verification, and Governance

The fourth layer is AI Spec Coding. Spec coding in AIAUF follows four steps:

1. The agent writes a **specification** based on the approved requirement (stating the problem, expected behavior, affected files, non-goals, risks, and acceptance criteria)
2. The agent writes an **implementation plan**, breaking the work into small tasks and identifying tests
3. The agent **implements** the change using test-driven or verification-driven development
4. The agent runs **fresh verification** before claiming completion

The governance layer then decides whether an implemented change can be released, personalized, simulated, or rejected. Some feedback may justify a global product update; other feedback may only justify a personal setting, a prompt adjustment, or a local memory update.

---

## 4. Chronological Workflow of the AIAUF Framework

### 4.1 Operational Overview

The workflow begins with user experience rather than provider assumptions. AIAUF reorganizes the conventional feedback process into a continuous but governed loop:

1. AI interviewers collect user feedback through adaptive conversations
2. An AI research agent cleans, codes, and distills feedback into structured requirements
3. A governance step determines whether a suggestion should be rejected, deferred, personalized, investigated, or approved
4. MCP-based context orchestration connects the approved requirement with relevant product documents, code repositories, tools, tests, and policies
5. AI spec coding converts the requirement into a testable implementation plan
6. The implemented change is verified and recorded as part of the agent's future memory, workflow, or product behavior

### 4.2 Stage 1: User Selection, Consent, and Adaptive AI Interviewing

Before the interview begins, the system should define the user group, sampling logic, consent statement, interview topic, and privacy boundary. The interview should state what feedback is being collected, how it will be used, and whether the user can stop.

**Code Listing 4.1. Interview Loop**

```typescript
type InterviewState = {
  messages: Message[];
  userProblem?: string;
  unresolvedPoints: string[];
  turnCount: number;
  stopReason?: "sufficient_detail" | "user_exit" | "max_turns";
};

async function interviewLoop(state: InterviewState) {
  while (!state.stopReason) {
    const nextQuestion = planFollowUp(state.messages, state.unresolvedPoints);
    const answer = await askUser(nextQuestion);
    state.messages.push(answer);
    state = updateInterviewState(state);
    if (hasEnoughEvidence(state) || state.turnCount >= 8) {
      state.stopReason = hasEnoughEvidence(state)
        ? "sufficient_detail"
        : "max_turns";
    }
  }
  return state;
}
```

AIAUF should include checks for short answers, unresolved complaints, repeated "I do not know" responses, missing context, and emotionally charged feedback. Interviews that fail these checks should be flagged for another round or human review.

### 4.3 Stage 2: Feedback Cleaning, Coding, and Requirement Distillation

Raw feedback is usually not implementation-ready. A user may say "the agent is useless," but the actual issue may be slow response, poor memory, weak follow-up, unclear interface, or mismatch with the user's work process. The distillation process includes transcript cleaning, segmentation, theme identification, feedback classification, evidence linking, and requirement drafting.

**Code Listing 4.2. Requirement object for distillation**

```json
{
  "requirement_id": "REQ-042",
  "feedback_type": "usability_problem",
  "user_problem": "Users cannot understand why the agent stops asking follow-up questions.",
  "evidence": ["INT-018", "INT-026", "INT-044"],
  "affected_module": "AI interviewer stopping logic",
  "severity": "medium",
  "frequency": 17,
  "risk_level": "low",
  "recommended_action": "Revise follow-up and stopping rules",
  "review_status": "pending_governance"
}
```

This structure preserves traceability. A feedback-analysis skill can define how to distinguish a complaint from a feature request. A safety skill can identify feedback that should not be implemented automatically. Memory allows the system to compare new findings with earlier rejected proposals, approved improvements, and post-release results.

### 4.4 Stage 3: Prioritization and Governance Gate

Not every suggestion should become an agent improvement. Some suggestions are valuable only for a small segment. Some are contradictory. Some would increase risk, reduce usability for other users, or violate product policy. The governance gate evaluates each requirement using criteria such as: evidence strength, user value, frequency, severity, technical feasibility, safety risk, privacy risk, cost, and strategic fit.

The decision should not be binary. A requirement may be:
- Approved for **global release**
- Approved only as a **personalized setting**
- Sent for **further investigation**
- **Deferred**
- **Rejected**

### 4.5 Stage 4: MCP-Based Context Orchestration

After approval, the requirement must relate to the technical environment. Through MCP or a similar tool protocol, the system can define what each agent is allowed to access, what it retrieved, and what action it performed. Context selection should be minimal rather than exhaustive — if the requirement concerns the AI interviewer's stopping logic, the coding agent may need the requirement object, several anonymized interview examples, the current interview prompt, the state schema, and relevant tests. It does not need private demographic details or unrelated complaints.

### 4.6 Stage 5: AI Spec Coding and Verification-Driven Implementation

The coding agent should not directly modify the system from raw user feedback. It should first write a specification:

**Code Listing 4.3. Brief spec template for AI spec coding**

```
# Spec ID: SPEC-042

Problem:
  The interviewer sometimes stops before the user explains the cause of dissatisfaction.

Expected behavior:
  Ask one clarification question when the answer is vague, severe, or contradictory.

Affected module:
  Interview follow-up planner and stopping rule.

Non-goal:
  Do not increase the maximum interview length for all users.

Acceptance criteria:
  1. Vague negative answers trigger a clarification question.
  2. Clear and complete answers can still close normally.
  3. Existing consent and privacy rules remain unchanged.
```

The implementation then follows the specification. The coding agent updates only the relevant module, writes or updates tests, runs verification, and reports whether acceptance criteria are satisfied.

### 4.7 Stage 6: Verification, Release Decision, and Continuous Self-Improvement

Verification may include unit tests, integration tests, benchmark comparison, safety review, human review, simulation, or limited release. After verification, the system records the outcome in memory. If the change succeeds, the requirement, specification, implementation summary, test result, and release decision become part of the improvement history. If the change fails, the system records why it failed, so that later agents do not repeat the same path.

After release or simulation, users may experience the modified agent and provide new feedback. The system can compare new feedback with earlier complaints and evaluate whether the improvement actually reduced the problem. In this way, AIAUF supports continuous adaptation, but its adaptation remains bounded by evidence, context control, specification, verification, and governance.

---

## 5. Discussion: Contributions, Evaluation, and Future Directions

### 5.1 Synthesis of the AIAUF Framework Contribution

AIAUF's main contribution is not that it introduces AI interviewing, agent self-improvement, MCP, or spec coding as isolated techniques — each of these already appears in existing literature. Rather, AIAUF connects them into a single feedback-to-improvement loop: AI interviewers collect user experience, research agents distill raw feedback into structured requirements, MCP-based infrastructure connects those requirements with technical context, and spec coding transforms approved requirements into testable implementation plans.

The framework also follows the human-centered AI position discussed by Jiang et al. (2024). As AI systems move from cooperative intelligence toward more autonomous forms of action, the need for feedback does not disappear — it becomes more important, because autonomous agents may influence user trust, workflow quality, decision expectations, and perceived accountability. AIAUF therefore treats self-improvement as a socio-technical process rather than a purely technical optimization loop.

### 5.2 Comparative Positioning Against Existing Approaches

**Compared with traditional surveys**, AIAUF provides a richer channel for collecting user experience, while still acknowledging the limitations of AI interviewing identified by Wong et al. (2025) and Wuttke et al. (2025). Feedback must pass through coding, distillation, contradiction checking, governance, and technical verification — making AIAUF different from simple feedback collection systems.

**Compared with agent self-improvement without user feedback**, AIAUF adds an external human-centered signal. Test-Time Recursive Thinking, EvoTest, and related methods show that agents can improve through candidate generation, evaluation, and memory updating (He et al., 2026; Zhuang et al., 2026), but they do not by themselves answer whether the improvement reflects user needs.

**Compared with loose vibe coding**, AIAUF also introduces stronger implementation control. Spec coding is more suitable for AIAUF because it requires a structured specification, acceptance criteria, test plan, and verification before implementation (Marri, 2026).

### 5.3 Evaluation Framework for AIAUF

AIAUF should be evaluated at four levels: feedback collection, feedback distillation, implementation quality, and system-level outcome.

At the **feedback collection level**, indicators include answer length, topic coverage, follow-up quality, unresolved complaint rate, participant satisfaction, and cross-language consistency.

At the **distillation level**, evaluation should focus on traceability and actionability:

**Code Listing 5.1. Requirement trace items**

```
RequirementTrace = {
  feedback_id,
  user_segment,
  evidence_summary,
  theme_code,
  proposed_requirement,
  risk_flag,
  governance_decision,
  spec_id,
  test_id,
  release_outcome
}
```

At the **implementation level**, AIAUF should be evaluated by specification completeness, test pass rate, regression rate, safety review result, and human review agreement.

At the **system level**, indicators include time from feedback to approved requirement, repeated complaint reduction, post-release user satisfaction, personalization accuracy, and the rate of rejected or reversed updates.

### 5.4 Limitations and Risks

AIAUF has several limitations:

1. The present article proposes a framework rather than a deployed production system — its effectiveness still requires case studies, prototypes, and controlled comparisons.
2. AI interviewing remains methodologically fragile. AIAUF therefore requires interview quality checks and human review for sensitive or low-quality interviews.
3. Large-scale feedback may still fail to represent niche users. Frequent complaints may dominate rare but important needs.
4. Self-improvement can create governance risks. Shao et al. (2026) warn that memory accumulation, tool creation, model updates, and workflow changes may lead to misevaluation. User feedback should therefore be treated as evidence, not as an automatic command.

### 5.5 Implications for Future Research

Future research should:

1. Implement AIAUF in a bounded software or agent environment and compare it with conventional feedback pipelines
2. Develop evaluation criteria for AI-conducted social research, combining traceability, auditability, triangulation, user confirmation, contradiction handling, and downstream outcome measurement
3. Design personalized self-improvement systems that decide whether a finding supports global release, segment-specific adaptation, local memory update, or rejection
4. Study the evolution of MCP-based infrastructure toward dynamic server discovery, with careful attention to access control, logging, and accountability

---

## 6. Conclusion

This study proposed the AI Agents Self-Improvement with User Feedback framework as a governed way to convert user experience into controlled agent improvement. The framework begins with adaptive AI interviewing, but it does not treat user comments as direct commands for system change. Feedback is cleaned, coded, clustered, and translated into traceable requirements before it relates to product context through MCP-based infrastructure. Approved requirements are implemented through spec coding, tested, reviewed, and recorded for evaluation.

The value of AIAUF lies in its integration of methods across user research, agent architecture, and software engineering. AI interviewing supports collection of qualitative evidence. Research agents, skills, and memory support interpretation and continuity. MCP supports access to technical context. Spec coding and governance reduce the risk that useful feedback becomes unsafe, unsuitable, or unverifiable modification.

This article should be understood as a framework and design proposal rather than evidence of production performance. Future work should examine interview quality, requirement traceability, implementation accuracy, post-release outcomes, and the distinction between global updates and personalized adaptation. AIAUF offers a structured path for making agent self-improvement more responsive to users while remaining accountable to verification and governance.

---

## References

Alsalloum, G., Badr, Y., Alzaatreh, A., Shamayleh, A., Kumail, M., Ahmad, N. A., & Hadjiat, Y. (2026). Acceptance and readiness for AI among United Arab Emirates–based health care practitioners: Exploratory cross-sectional survey. *JMIR AI*, *5*, e80173.

Anthropic. (2025). *What 81,000 people want from AI*. https://www.anthropic.com/features/81k-interviews

Anthropic. (2026, April 22). Building agents that reach production systems with MCP. *Claude*. https://claude.com/blog/building-agents-that-reach-production-systems-with-mcp

Balis, B., Orzechowski, M., Kica, P., Dygas, M., & Kuszewski, M. (2026). *From research question to scientific workflow: Leveraging agentic AI for science automation* (arXiv:2604.21910). arXiv. https://doi.org/10.48550/arXiv.2604.21910

Benda, N., Desai, P., Reza, Z., Winogora, V., Suresh, U., Zhang, Y., Hermann, A., Joly, R., Pathak, J., & Reading Turchioe, M. (2026). A qualitative interview study investigating patient, health professional, and developer perspectives on real-world implementation of patient-centered AI systems. *npj Digital Medicine*, *9*(1), 352.

Berger, P., & Luckmann, T. (2016). The social construction of reality. In *Social theory re-wired* (pp. 110–122). Routledge.

Besanson, G. (2026). The inference bottleneck: A formal model of vertical foreclosure in AI markets. *arXiv preprint arXiv:2604.17431*. https://arxiv.org/abs/2604.17431

Borthwick, A., & Ash, S. (2026). *RoboPhD: Self-improving text-to-SQL through autonomous agent evolution* (arXiv:2601.01126). arXiv. https://doi.org/10.48550/arXiv.2601.01126

Cronbach, L. J. (1951). Coefficient alpha and the internal structure of tests. *Psychometrika*, *16*(3), 297–334.

Cronbach, L. J., & Meehl, P. E. (1955). Construct validity in psychological tests. *Psychological Bulletin*, *52*(4), 281.

Daniel, M. (2026, April 2). *Superpowers for spec-first AI coding*. Spec Coding. https://spec-coding.dev/blog/superpowers-spec-first-ai-agent-skills

Fang, J., Peng, Y., Zhang, X., Wang, Y., Yi, X., Zhang, G., Xu, Y., Wu, B., Liu, S., Li, Z., Ren, Z., Aletras, N., Wang, X., Zhou, H., & Meng, Z. (2025). *A comprehensive survey of self-evolving AI agents: A new paradigm bridging foundation models and lifelong agentic systems* (arXiv:2508.07407). arXiv. https://doi.org/10.48550/arXiv.2508.07407

Grossmann, I., Feinberg, M., Parker, D. C., Christakis, N. A., Tetlock, P. E., & Cunningham, W. A. (2023). AI and the transformation of social science research. *Science*, *380*(6650), 1108–1109. https://doi.org/10.1126/science.adi1778

Gruber, J., & Hilgert, J.-N. (2026). *Foundations for agentic AI investigations from the forensic analysis of OpenClaw* (arXiv:2604.05589). arXiv. https://doi.org/10.48550/arXiv.2604.05589

Gulliksen, H. (2013). *Theory of mental tests*. Routledge.

He, Y., Liu, J., Liu, Y., Li, Y., Cao, T., Hu, Z., Xu, X., & Hooi, B. (2026). *EvoTest: Evolutionary test-time learning for self-improving agentic systems* (arXiv:2510.13220). arXiv. https://doi.org/10.48550/arXiv.2510.13220

Jiang, T., Sun, Z., Fu, S., & Lv, Y. (2024). Human-AI interaction research agenda: A user-centered perspective. *Data and Information Management*, *8*(4), 100078.

Khojasteh, L., Karimian, Z., Nasiri, E., Kafipour, R., & Farahmandi, A. Y. (2025). Artificial intelligence and academic writing questionnaire (AI-AWQ): Development and validation among medical students' experiences using exploratory factor analysis. *BMC Medical Education*, *25*(1), 1697. https://doi.org/10.1186/s12909-025-08288-z

Lance, M., Gabe, C., & Michael, C. (2026, April 8). *Scaling managed agents: Decoupling the brain from the hands*. https://www.anthropic.com/engineering/managed-agents

Lin, W. (2026, March 30). *How Claude Code works*. https://wanlanglin.github.io/-awesome-cc-harness/

Lindgren, H. (2025). Emerging roles and relationships among humans and interactive AI systems. *International Journal of Human–Computer Interaction*, *41*(17), 10595–10617. https://doi.org/10.1080/10447318.2024.2435693

Liu, M., Liang, K., Zhao, Y., Tu, W., Zhou, S., Gan, X., Liu, X., & He, K. (2024). Self-supervised temporal graph learning with temporal and structural intensity alignment. *IEEE Transactions on Neural Networks and Learning Systems*, *36*(4), 6355–6367.

Liu, S., Fang, J., Zhou, H., Wang, Y., & Meng, Z. (2026). *SEW: Self-evolving agentic workflows for automated code generation* (arXiv:2505.18646). arXiv. https://doi.org/10.48550/arXiv.2505.18646

Mahdi, H. (2026). *Perceive, plan, act, self-correct: An architectural framework for goal-directed agentic AI systems*. https://engrxiv.org/preprint/view/6738

Marri, S. R. (2026). *Constitutional spec-driven development: Enforcing security by construction in AI-assisted code generation* (arXiv:2602.02584). arXiv. https://doi.org/10.48550/arXiv.2602.02584

Meske, C., Hermanns, T., Von der Weiden, E., Loser, K.-U., & Berger, T. (2025). Vibe coding as a reconfiguration of intent mediation in software development: Definition, implications, and research agenda. *IEEE Access*, *13*, 213242–213259.

Mukkolakkal, M. R. C. (2026). *Deploy, calibrate, monitor, heal — no human required: An autonomous AI SRE agent for Elasticsearch* (arXiv:2604.03933). arXiv. https://doi.org/10.48550/arXiv.2604.03933

Narajala, V. S., & Habler, I. (2026). Enterprise-grade security for the model context protocol (MCP): Frameworks and mitigation strategies. *2026 IEEE 5th International Conference on AI in Cybersecurity (ICAIC)*, 1–8. https://ieeexplore.ieee.org/abstract/document/11395723/

Orlikowski, W. J., & Baroudi, J. J. (1991). Studying information technology in organizations: Research approaches and assumptions. *Information Systems Research*, *2*(1), 1–28. https://doi.org/10.1287/isre.2.1.1

Riley, C., Al-Refai, O., Reyes, Y. C., & Hammad, E. (2025). Human-AI interactions: Cognitive, behavioral, and emotional impacts. *arXiv preprint arXiv:2510.17753*. https://arxiv.org/abs/2510.17753

Sapkota, R., Roumeliotis, K. I., & Karkee, M. (2025). AI agents vs. agentic AI: A conceptual taxonomy, applications and challenges. *Information Fusion*, 103599.

Shao, S., Ren, Q., Qian, C., Wei, B., Guo, D., Yang, J., Song, X., Zhang, L., Zhang, W., Liu, D., & Shao, J. (2026). *Your agent may misevolve: Emergent risks in self-evolving LLM agents* (arXiv:2509.26354). arXiv. https://doi.org/10.48550/arXiv.2509.26354

Terry, J., Strait, G., Alsarraf, S., Weinmann, E., & Waychoff, A. (2025). Artificial intelligence in scale development: Evaluating AI-generated survey items against gold standard measures. *Current Psychology*, *44*(20), 16339–16350. https://doi.org/10.1007/s12144-025-08240-w

Wang, C., Zhang, Y., Yu, R., Zheng, Y., Gao, L., Song, Z., Xu, Z., Xia, G., Zhang, H., Zhao, D., & Chen, X. (2025). *Do LLMs 'feel'? Emotion circuits discovery and control* (arXiv:2510.11328). arXiv. https://doi.org/10.48550/arXiv.2510.11328

Wen, Y., Zhang, Y., Suresh, S., Lu, Z., Liu, C., & Xia, M. (2026). InterFlow: Designing unobtrusive AI to empower interviewers in semi-structured interviews. *Proceedings of the 2026 CHI Conference on Human Factors in Computing Systems*, 1–21. https://doi.org/10.1145/3772318.3790866

Wong, L. Z., Juraimi, S. A., Tan, Y. Z., Loh, S. B., Chong, M. F., Bhattacharya, P., & Pink, A. E. (2025). The AI interviewer: Exploring the use of conversational AI-enabled chatbots in qualitative data collection. *Available at SSRN 5194078*. https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5194078

Wuttke, A., Aßenmacher, M., Klamm, C., Lang, M. M., Würschinger, Q., & Kreuter, F. (2025). AI conversational interviewing: Transforming surveys with LLMs as adaptive interviewers. *Proceedings of the 9th Joint SIGHUM Workshop on Computational Linguistics for Cultural Heritage, Social Sciences, Humanities and Literature (LaTeCH-CLfL 2025)*, 179–204. https://aclanthology.org/2025.latechclfl-1.17/

Xie, Y., Liang, L., Li, S., Lu, Y., Xiao, Z., Shi, M., Huang, J., Wang, M., & Xie, Y. (2026). Evaluating the statistical realism of LLM-generated social science data. *Proceedings of the National Academy of Sciences*, *123*(19), e2538145123. https://doi.org/10.1073/pnas.2538145123

Xu, B. (2026). AI agent systems: Architectures, applications, and evaluation. *arXiv preprint arXiv:2601.01743*. https://arxiv.org/abs/2601.01743

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K. R., & Cao, Y. (2022). ReAct: Synergizing reasoning and acting in language models. *The Eleventh International Conference on Learning Representations*. https://openreview.net/forum?id=WE_vluYUL-X

Yuma Heymans. (2026, March 26). *Self-improving AI agents: The 2026 guide*. https://o-mega.ai/articles/self-improving-ai-agents-the-2026-guide

Zhuang, Y., Singh, C., Liu, L., Shen, Y., Zhang, D., Shang, J., Gao, J., & Chen, W. (2026). *Test-time recursive thinking: Self-improvement without external feedback* (arXiv:2602.03094). arXiv. https://doi.org/10.48550/arXiv.2602.03094
