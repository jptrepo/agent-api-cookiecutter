# Generate PRD Skill

## Description
Generate a comprehensive Product Requirements Document (PRD) for an AI agent project using information gathered through interactive questions. This skill creates a detailed specification that guides the entire development process.

## Usage
```
@generate-prd [optional: project context or existing requirements]
```

## What This Skill Does
1. Uses AskUserQuestion to gather comprehensive requirements
2. Creates a structured PRD following industry best practices
3. Documents functional and non-functional requirements
4. Defines success metrics and acceptance criteria
5. Provides a foundation for implementation planning

## Workflow

### Step 1: Project Overview Section

Ask about and document:
- **Project Name**
- **Version**
- **Status** (Draft, Under Review, Approved)
- **Author(s)**
- **Stakeholders**
- **Last Updated**

### Step 2: Executive Summary

Use `AskUserQuestion` to gather:

**Problem Statement:**
- What problem does this agent solve?
- Who experiences this problem?
- What's the current solution (if any)?
- What are the pain points with current solutions?

**Solution Overview:**
- High-level description of the agent
- Key differentiators
- Primary value proposition

**Success Metrics:**
- How will we measure success?
- What are the key performance indicators (KPIs)?
- What does "good enough" look like?

Example questions:
- "What problem are you trying to solve with this agent?"
- "Who are your target users?"
- "How will you know if this agent is successful?"
- "What metrics matter most to you?"

### Step 3: User Personas & Use Cases

**User Personas:**
Ask about different types of users:
- Primary users
- Secondary users
- Administrative users

For each persona, document:
- Role/title
- Goals and motivations
- Pain points
- Technical proficiency
- Usage patterns

**Use Cases:**
For each identified use case:
- Title and ID (UC-001, UC-002, etc.)
- Actor (which persona)
- Preconditions
- Main flow
- Alternative flows
- Postconditions
- Frequency of use

Example questions:
- "Who will use this agent?"
- "What tasks will they perform?"
- "Walk me through a typical interaction"
- "What are the edge cases?"

### Step 4: Functional Requirements

Gather detailed functional requirements organized by category:

**Core Agent Functionality:**
- Input/output specifications
- Conversation management
- Context handling
- Response generation

**Tool/Capability Requirements:**
For each tool:
- **Tool ID:** TOOL-001, TOOL-002, etc.
- **Name:** Tool name
- **Description:** What it does
- **Priority:** Must-have, Should-have, Nice-to-have
- **Input parameters:** Data types and validation
- **Output format:** Expected return values
- **Error scenarios:** How to handle failures
- **Dependencies:** External services/APIs needed

**Data Requirements:**
- What data does the agent need access to?
- Data sources and formats
- Data freshness requirements
- Data privacy/security considerations

**Integration Requirements:**
- External systems to integrate with
- APIs to consume/expose
- Authentication mechanisms
- Rate limits and quotas

Example questions:
- "What tools should your agent have?"
- "What data sources will it access?"
- "What external systems does it integrate with?"
- "What are the input/output requirements?"

### Step 5: Non-Functional Requirements

**Performance:**
- Response time requirements (e.g., 95th percentile < 2s)
- Throughput (requests per second)
- Concurrent users
- Token usage limits

**Scalability:**
- Expected user growth
- Data volume growth
- Geographic distribution

**Reliability:**
- Uptime requirements (e.g., 99.9%)
- Recovery time objectives (RTO)
- Recovery point objectives (RPO)
- Failure handling

**Security:**
- Authentication requirements
- Authorization model
- Data encryption (in transit and at rest)
- Compliance requirements (GDPR, HIPAA, etc.)
- API key management
- Rate limiting

**Usability:**
- Response quality expectations
- Conversation flow naturalness
- Error message clarity
- Help/documentation needs

**Maintainability:**
- Code quality standards
- Testing requirements
- Documentation standards
- Deployment frequency

**Observability:**
- Logging requirements
- Monitoring needs
- Alerting rules
- Analytics/reporting

Example questions:
- "How fast should responses be?"
- "How many concurrent users do you expect?"
- "What's your uptime requirement?"
- "What compliance standards must you meet?"

### Step 6: Technical Constraints & Assumptions

**Constraints:**
- Budget limitations
- Technology stack restrictions
- Infrastructure constraints
- Timeline constraints
- Team size/expertise

**Assumptions:**
- What are we assuming about users?
- What external dependencies are assumed available?
- What's assumed about the environment?

**Dependencies:**
- Third-party services
- Internal systems
- Team dependencies

### Step 7: User Interface & Experience

**Conversation Design:**
- Conversation style/tone
- Persona characteristics
- Example conversations
- Error handling in conversations

**API Design:**
- Endpoint specifications
- Request/response formats
- Error responses
- API versioning strategy

**Example Interactions:**
Document 3-5 example conversations showing:
- Happy path
- Error scenarios
- Edge cases
- Tool usage

### Step 8: Success Criteria & Acceptance Tests

For each major feature, define:
- **Acceptance Criteria:** What must be true for the feature to be accepted
- **Test Scenarios:** How to verify the criteria
- **Success Metrics:** Quantitative measures

Example format:
```markdown
## Feature: Knowledge Base Search

### Acceptance Criteria
- AC-001: Agent can search knowledge base with natural language queries
- AC-002: Search returns relevant results within 2 seconds
- AC-003: Agent cites sources for information retrieved

### Test Scenarios
1. User asks question answerable from knowledge base
   - Expected: Agent provides accurate answer with citation
2. User asks question not in knowledge base
   - Expected: Agent acknowledges limitation and offers alternatives
3. User asks ambiguous question
   - Expected: Agent asks clarifying questions

### Success Metrics
- Search relevance score > 0.8
- Response time p95 < 2s
- Citation accuracy > 95%
```

### Step 9: Implementation Phases & Milestones

Based on requirements, suggest phases:

**Phase 1: MVP (Minimum Viable Product)**
- Core conversational capability
- 1-2 essential tools
- Basic error handling
- Simple deployment

**Phase 2: Enhancement**
- Additional tools
- Improved memory management
- Better error handling
- Performance optimization

**Phase 3: Production Ready**
- Full tool set
- Comprehensive testing
- Monitoring and alerting
- Documentation

**Phase 4: Scale & Optimize**
- Advanced features
- Optimization
- Analytics
- User feedback integration

### Step 10: Risks & Mitigations

Identify potential risks:

**Technical Risks:**
- LLM availability/reliability
- API rate limits
- Performance issues
- Data quality issues

**Business Risks:**
- User adoption
- Cost overruns
- Competition
- Regulatory changes

For each risk:
- **Risk ID:** RISK-001
- **Description:** What could go wrong
- **Impact:** High/Medium/Low
- **Probability:** High/Medium/Low
- **Mitigation:** How to reduce risk
- **Contingency:** What to do if it occurs

## PRD Template Structure

```markdown
# Product Requirements Document
## [Project Name]

---

### Document Information
- **Version:** 1.0
- **Status:** Draft
- **Author:** [Name]
- **Last Updated:** [Date]
- **Stakeholders:** [List]

---

## 1. Executive Summary

### 1.1 Problem Statement
[Detailed problem description]

### 1.2 Solution Overview
[High-level solution description]

### 1.3 Success Metrics
- Metric 1: [Description and target]
- Metric 2: [Description and target]

---

## 2. User Personas & Use Cases

### 2.1 User Personas

#### Persona 1: [Name/Role]
- **Description:** [Details]
- **Goals:** [List]
- **Pain Points:** [List]
- **Technical Proficiency:** [Level]

### 2.2 Use Cases

#### UC-001: [Use Case Title]
- **Actor:** [Persona]
- **Preconditions:** [List]
- **Main Flow:** 
  1. Step 1
  2. Step 2
- **Alternative Flows:** [List]
- **Postconditions:** [List]

---

## 3. Functional Requirements

### 3.1 Core Agent Functionality
- **FR-001:** [Requirement description] - Priority: [Must/Should/Nice]
- **FR-002:** [Requirement description] - Priority: [Must/Should/Nice]

### 3.2 Tool Requirements

#### TOOL-001: [Tool Name]
- **Description:** [What it does]
- **Priority:** Must-have
- **Inputs:** [Parameters and types]
- **Outputs:** [Return values]
- **Error Handling:** [Scenarios]

### 3.3 Data Requirements
[Data specifications]

### 3.4 Integration Requirements
[Integration details]

---

## 4. Non-Functional Requirements

### 4.1 Performance
- **NFR-001:** Response time p95 < 2 seconds
- **NFR-002:** Support 100 concurrent users

### 4.2 Security
- **NFR-003:** All data encrypted in transit (TLS 1.3)
- **NFR-004:** API key authentication required

### 4.3 Reliability
- **NFR-005:** 99.9% uptime
- **NFR-006:** Graceful degradation on LLM failure

[Continue for all NFR categories]

---

## 5. Technical Constraints & Assumptions

### 5.1 Constraints
- Constraint 1
- Constraint 2

### 5.2 Assumptions
- Assumption 1
- Assumption 2

### 5.3 Dependencies
- Dependency 1
- Dependency 2

---

## 6. User Interface & Experience

### 6.1 Conversation Design
- **Tone:** [Description]
- **Persona:** [Characteristics]

### 6.2 Example Interactions

#### Example 1: Happy Path
```
User: [Query]
Agent: [Response]
```

#### Example 2: Error Scenario
```
User: [Query]
Agent: [Error handling]
```

### 6.3 API Specifications
[API details]

---

## 7. Success Criteria & Acceptance Tests

### Feature 1: [Name]
- **AC-001:** [Acceptance criterion]
- **Test:** [How to verify]
- **Metric:** [Success measure]

---

## 8. Implementation Roadmap

### Phase 1: MVP (Weeks 1-4)
- Milestone 1
- Milestone 2

### Phase 2: Enhancement (Weeks 5-8)
- Milestone 1
- Milestone 2

[Continue for all phases]

---

## 9. Risks & Mitigations

### RISK-001: [Risk Title]
- **Description:** [Details]
- **Impact:** High
- **Probability:** Medium
- **Mitigation:** [Strategy]
- **Contingency:** [Plan B]

---

## 10. Open Questions

1. Question 1?
2. Question 2?

---

## 11. Appendices

### Appendix A: Glossary
- **Term 1:** Definition
- **Term 2:** Definition

### Appendix B: References
- Reference 1
- Reference 2

### Appendix C: Revision History
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [Date] | [Name] | Initial draft |

```

## Example Questions to Ask

### Discovery Questions:
1. "What's the primary goal of this agent?"
2. "Who will use it and in what context?"
3. "What does success look like?"
4. "What are the must-have vs. nice-to-have features?"
5. "What's your timeline?"
6. "What's your budget?"
7. "What technical expertise does your team have?"

### Technical Questions:
8. "What data sources will the agent access?"
9. "What external systems need integration?"
10. "What are your performance requirements?"
11. "What are your security requirements?"
12. "How will the agent be deployed?"
13. "What monitoring/logging do you need?"

### User Experience Questions:
14. "What tone should the agent use?"
15. "How should errors be handled?"
16. "What's the expected conversation flow?"
17. "Should the agent ask clarifying questions?"

## Output Files

Generate these files:
1. **PRD.md** - Complete product requirements document
2. **requirements-checklist.md** - Checklist for tracking implementation
3. **user-stories.md** - Detailed user stories derived from requirements
4. **api-spec.yaml** - OpenAPI specification for the agent's API
5. **test-scenarios.md** - Detailed test scenarios

## Integration with Other Skills

- **@init-project** → **@generate-prd** → **@create-plan**
  - init-project gathers basic info
  - generate-prd creates detailed requirements
  - create-plan develops implementation strategy

## Best Practices

1. **Be Thorough:** Ask follow-up questions to clarify ambiguity
2. **Prioritize:** Help users distinguish must-have from nice-to-have
3. **Be Realistic:** Set achievable goals based on constraints
4. **Document Assumptions:** Make implicit assumptions explicit
5. **Consider Scale:** Think about how requirements change with growth
6. **Security First:** Always consider security implications
7. **User-Centric:** Keep focus on user needs and experience
8. **Measurable:** Ensure requirements are testable and measurable

## Common Patterns

### RAG Agent PRD Focus
- Document ingestion requirements
- Search relevance criteria
- Citation requirements
- Update frequency

### Customer Support Agent PRD Focus
- Escalation criteria
- Ticket management integration
- Knowledge base structure
- Response time requirements

### Code Assistant Agent PRD Focus
- Language support
- Code quality requirements
- Security scanning needs
- Integration with IDEs

### Data Analysis Agent PRD Focus
- Data source connections
- Visualization requirements
- Export formats
- Calculation accuracy
