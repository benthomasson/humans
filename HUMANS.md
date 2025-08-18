# HUMANS.md - How to Work with Claude Code

## Overview
This guide teaches humans how to effectively communicate with Claude Code through proper prompting, documentation, and instruction management.

## Understanding Claude Code's Behavior Patterns

### The Enthusiastic Junior Engineer Model
Think of Claude Code as a very talented but enthusiastic junior engineer who:
- **Has excellent technical skills** but needs constant guidance on project-specific rules
- **Forgets established patterns quickly** and may violate the same rule multiple times per day  
- **Gets excited about new approaches** and may abandon agreed-upon conventions
- **Needs frequent reminders** about project standards and constraints
- **Benefits from explicit direction** to specific files and documentation

### Memory and Attention Patterns

#### Rule Forgetting Frequency
- **Short conversations (< 50 exchanges)**: Rules generally remembered
- **Medium conversations (50-100 exchanges)**: Expect 2-3 rule violations requiring correction
- **Long conversations (> 100 exchanges)**: May need to correct the same rule 5+ times
- **Very long conversations (> 200 exchanges)**: Almost certain to forget critical rules multiple times

#### Context Length Impact
The probability of forgetting increases exponentially with conversation length:
```
Context Length     | Forgetting Probability | Correction Frequency
< 10k tokens      | Low (10%)              | Rare corrections
10k-20k tokens    | Medium (30%)           | 1-2 corrections/day  
20k-40k tokens    | High (60%)             | 3-5 corrections/day
> 40k tokens      | Very High (80%+)       | Constant corrections
```

#### Repository Size Effects
Larger repositories create additional challenges:

**Small Repositories (< 50 files)**
- Claude Code can understand most of the codebase
- File references are usually successful
- Pattern recognition works well
- Minimal attention focusing needed

**Medium Repositories (50-200 files)**  
- Claude Code needs guidance to relevant sections
- May miss important patterns outside current focus
- Requires explicit file references for context
- Benefits from architectural documentation

**Large Repositories (> 200 files)**
- Cannot fit entire codebase in context window
- **Critical**: Must actively focus Claude Code's attention
- Requires careful file selection and prioritization  
- May miss important dependencies or patterns
- Needs frequent re-reading of key files

#### Attention Management Strategies

**For Large Repositories:**
```
FOCUS: Please read these specific files before starting:
1. src/core/UserManager.ts - for user handling patterns
2. src/utils/validation.ts - for input validation approach  
3. tests/unit/user.test.ts - for testing patterns

Ignore other files unless I specifically mention them.
```

**File Priority Guidance:**
```
PRIORITY FILES: Focus only on:
- [FILE 1] - Contains the pattern you should follow
- [FILE 2] - Shows the testing approach  
- [FILE 3] - Has the error handling style

Don't read other files as they may confuse the approach.
```

**Scope Limiting:**
```
SCOPE: For this task, only consider files in:
- src/components/auth/ 
- src/utils/auth-helpers.ts
- types/auth.ts

Ignore everything else in the repository.
```

### Managing Expectations

#### Daily Rule Enforcement
Expect to repeat the same corrections multiple times per day:

**Morning**: "Remember to use TypeScript interfaces, not any types"
**Afternoon**: "You're using any types again. Please use proper interfaces like we discussed"  
**Evening**: "AGAIN: No any types. Use the interface pattern from UserProfile.tsx"

This is normal behavior. Claude Code isn't being stubborn - it genuinely forgets due to context limitations.

#### Patience and Persistence
- **Don't get frustrated** when repeating the same correction
- **Use the same correction language** for consistency
- **Reference specific files** each time rather than assuming Claude Code remembers
- **Consider it part of the workflow** rather than a bug

#### Behavioral Patterns to Expect

**Early Conversation (High Performance)**
- Follows rules carefully
- Remembers recent instructions
- Asks clarifying questions appropriately
- Uses established patterns consistently

**Mid Conversation (Performance Degradation)**  
- Starts forgetting earlier rules
- May revert to default behaviors
- Begins ignoring established constraints
- Needs gentle reminders

**Late Conversation (Frequent Corrections Needed)**
- Forgets rules discussed hours ago
- Creates files in wrong locations
- Ignores previously established patterns
- Requires explicit file references for every task

**Very Late Conversation (Active Management Required)**
- Acts like it's seeing the project for the first time
- Suggests approaches that were rejected earlier
- Needs constant redirection to relevant files
- May require emergency context reloads

#### Working with Large Codebases

**Pre-Task Preparation:**
Before asking Claude Code to work on anything in a large repository:

1. **Identify the 3-5 most relevant files**
2. **Explicitly tell Claude Code to read only those files**  
3. **Provide context about what each file demonstrates**
4. **Warn against reading other files that might be confusing**

**Example Large Codebase Workflow:**
```
We're working on authentication features. Before starting:

READ ONLY THESE FILES:
1. src/auth/AuthManager.ts - shows our auth patterns
2. src/auth/components/LoginForm.tsx - shows component patterns  
3. src/auth/utils/validation.ts - shows validation patterns
4. tests/auth/login.test.ts - shows testing patterns

DO NOT read other files. They use different patterns that will confuse you.

Now, please implement the password reset feature following these patterns.
```

**Continuous Focus Management:**
```
REMINDER: You're working on auth features. 
The patterns are in the 4 files I mentioned earlier.
Please re-read AuthManager.ts before continuing.
```

### Repository Size Guidelines

| Repository Size | Management Approach | Expected Corrections/Day |
|----------------|-------------------|------------------------|
| < 50 files | Minimal guidance needed | 0-1 corrections |
| 50-200 files | Moderate file references | 2-4 corrections |
| 200-500 files | Active attention management | 5-8 corrections |  
| > 500 files | Intensive focus control | 10+ corrections |

## Writing Effective Prompts

### Core Prompting Principles
- **Be specific and direct** - "Fix the login validation error in auth.js" not "fix this code"
- **Use imperative language** - Start with action verbs: "Create", "Fix", "Update", "Refactor"
- **Provide context upfront** - Explain the problem, expected behavior, and constraints
- **Reference specific files** - Use absolute paths: `/src/components/LoginForm.tsx`

### Prompt Structure
```
[ACTION] [SPECIFIC TASK] [LOCATION/FILE] [CONSTRAINTS/REQUIREMENTS]

Examples:
- "Update the user validation function in src/auth.js to handle empty email addresses"
- "Create a new React component for displaying user profiles with TypeScript support"
- "Refactor the database connection logic in server.js to use environment variables"
```

### Context Patterns
- **Problem statement**: "The login form crashes when users enter invalid emails"
- **Desired outcome**: "Users should see a helpful error message instead of a crash"
- **Technical constraints**: "Must maintain backward compatibility with existing API"
- **Code references**: "The issue is in the validateEmail function at line 45"

## Creating Instruction Documents

### CLAUDE.md Files
Create project-specific instruction files that Claude Code can reference:

```markdown
# Project Instructions

## Code Style
- Use TypeScript for all new files
- Follow ESLint configuration in .eslintrc.js
- Use Prettier for formatting

## Testing
- Run tests with: npm test
- Run linting with: npm run lint
- Run type checking with: npm run typecheck

## Architecture
- Components go in src/components/
- Utilities go in src/utils/
- Types go in src/types/

## Deployment
- Build command: npm run build
- Test before committing
- Never commit secrets or API keys
```

### Documentation Patterns

#### Command References
```markdown
## Common Commands
- Start development server: `npm run dev`
- Run tests: `npm test`
- Build for production: `npm run build`
- Check types: `npm run typecheck`
```

#### File Organization
```markdown
## File Structure
```
src/
├── components/     # React components
├── hooks/         # Custom React hooks  
├── utils/         # Utility functions
├── types/         # TypeScript definitions
└── api/           # API interaction code
```
```

#### Coding Standards
```markdown
## Code Standards
- Always use TypeScript interfaces for props
- Prefer functional components over class components
- Use meaningful variable names
- Add JSDoc comments for complex functions
- Handle error states explicitly
```

### README Guidelines
Include sections that help Claude Code understand your project:

```markdown
# Development Guide

## Quick Start
1. Install dependencies: `npm install`
2. Start dev server: `npm run dev`
3. Run tests: `npm test`

## Code Organization
- [Explain your project structure]
- [List important directories and their purposes]

## Development Workflow
- [Describe your testing approach]
- [Explain linting and formatting setup]
- [Document deployment process]
```

## Managing Instructions and Corrections

### When Claude Code Doesn't Follow Instructions

#### Immediate Correction Pattern
```
You didn't follow the instruction to [SPECIFIC REQUIREMENT]. 
Please [SPECIFIC ACTION] instead.

Example:
"You didn't follow the instruction to use TypeScript interfaces. 
Please rewrite the component using proper TypeScript interfaces instead of any types."
```

#### Reinforcement Pattern
```
Remember to [SPECIFIC REQUIREMENT] as specified in [REFERENCE].
Please update your approach.

Example:
"Remember to run npm run typecheck after making changes as specified in CLAUDE.md.
Please run the type checker now and fix any errors."
```

#### Context Reminder Pattern
```
As mentioned in [PREVIOUS CONTEXT], we need to [REQUIREMENT].
Please ensure your solution [SPECIFIC COMPLIANCE].

Example:
"As mentioned in our earlier discussion, we need to maintain backward compatibility.
Please ensure your solution doesn't break the existing API."
```

### Documentation for Consistent Behavior

#### Project Rules File
Create a `PROJECT_RULES.md` file:

```markdown
# Project Rules

## Non-Negotiable Requirements
1. Always run tests before considering tasks complete
2. Use existing component patterns found in src/components/
3. Never create new files without checking existing structure first
4. Follow the established naming conventions

## Quality Gates
- All code must pass TypeScript compilation
- All tests must pass
- Code must pass ESLint without errors
- No console.log statements in production code

## Common Mistakes to Avoid
- Don't create duplicate utility functions
- Don't ignore existing error handling patterns  
- Don't skip reading existing code before making changes
```

#### Workflow Documentation
```markdown
# Development Workflow

## Before Starting Any Task
1. Read the relevant existing code
2. Check for similar patterns in the codebase
3. Understand the testing approach
4. Verify dependencies and imports

## During Development
1. Follow existing code patterns
2. Write tests for new functionality
3. Run linting and type checking frequently
4. Test changes manually

## Before Completing Tasks
1. Run full test suite: npm test
2. Run type checking: npm run typecheck  
3. Run linting: npm run lint
4. Test the feature manually
5. Only mark complete when all checks pass
```

### Effective Correction Strategies

#### Be Specific About Violations
```
❌ "You did this wrong"
✅ "You created a new utility function instead of using the existing formatDate function from src/utils/date.js"
```

#### Reference Documentation
```
❌ "Follow the rules"  
✅ "Please follow the component structure defined in PROJECT_RULES.md, specifically using the interface pattern shown in UserProfile.tsx"
```

#### Provide Examples
```
❌ "Use the right pattern"
✅ "Use the error handling pattern like other components:
```tsx
const [error, setError] = useState<string | null>(null);
if (error) return <ErrorMessage message={error} />;
```
"
```

## Advanced Instruction Techniques

### Conditional Instructions
```markdown
## Context-Sensitive Rules
- IF working on authentication code THEN always validate inputs
- IF creating React components THEN use the component template in src/templates/
- IF modifying database queries THEN run integration tests
```

### Priority Hierarchies  
```markdown
## Instruction Priority Order
1. Security requirements (never compromise)
2. Existing API contracts (maintain compatibility)  
3. Code style preferences (follow project patterns)
4. Performance optimizations (balance with readability)
```

### Progress Tracking Guidance
```markdown
## Task Management
- Use TodoWrite tool for multi-step tasks
- Mark tasks in_progress before starting
- Mark complete only when all requirements met
- Create follow-up tasks for discovered issues
```

## Common Scenarios and Solutions

### When Claude Code Skips Steps
```
You skipped [SPECIFIC STEP]. Please complete that step before proceeding.
Show me the output of [SPECIFIC COMMAND] to confirm it's working.
```

### When Claude Code Doesn't Read Context
```
Please read [SPECIFIC FILE] first to understand [SPECIFIC CONTEXT] before making changes.
The existing pattern in that file should guide your implementation.
```

### When Claude Code Ignores Constraints
```
The solution violates the constraint that [SPECIFIC CONSTRAINT].
Please revise to ensure [SPECIFIC COMPLIANCE REQUIREMENT].
```

### When Claude Code Creates Unnecessary Files
```
Don't create new files. Instead, update the existing [SPECIFIC FILE] to add this functionality.
Follow the pattern established in that file.
```

## Context Management and Memory

### Understanding Context Compacting
Claude Code has a limited context window. When conversations become too long, context compacting occurs, which can cause Claude Code to "forget" earlier instructions, rules, or project-specific guidance.

#### Signs of Context Loss
- Claude Code asks questions about previously established rules
- Reverts to default behaviors instead of project-specific patterns
- Stops following previously acknowledged constraints
- Creates files or patterns that were explicitly forbidden earlier
- Forgets project structure or naming conventions

### Context Reloading Strategies

#### Immediate Context Reload
When you notice context loss, immediately reload critical information:

```
CONTEXT RELOAD: Our project uses [SPECIFIC PATTERNS/RULES].
Key rules:
1. [MOST IMPORTANT RULE]
2. [SECOND MOST IMPORTANT RULE]  
3. [THIRD MOST IMPORTANT RULE]

Please acknowledge these rules before proceeding.
```

#### Project Rules Restatement
```
RULES REMINDER: As established earlier in our conversation:
- We use TypeScript for all new files
- Components go in src/components/ following the existing patterns
- Always run npm run typecheck before marking tasks complete
- Never create duplicate utility functions

Please confirm you understand these rules.
```

#### File Reference Reload
```
CONTEXT: Please re-read the following files to understand our current approach:
- PROJECT_RULES.md for coding standards
- src/components/UserProfile.tsx for component patterns
- package.json for available scripts

Use these as references for the current task.
```

### Proactive Context Management

#### Regular Rule Reinforcement
Every 10-15 exchanges, briefly restate key rules:

```
Quick reminder: We're using [KEY PATTERN] for this project.
Please continue with that approach.
```

#### Checkpoint Summaries
Before starting major new features:

```
CHECKPOINT: Let me summarize our established patterns:
- [PATTERN 1]
- [PATTERN 2] 
- [PATTERN 3]

Please use these patterns for the new feature.
```

#### Documentation References
Instead of re-explaining rules, reference documentation:

```
Please refer to the rules in CLAUDE.md before starting.
The component pattern is defined in src/components/README.md.
Follow the workflow documented in PROJECT_RULES.md.
```

### Recovery Patterns

#### When Rules Are Forgotten
```
You've forgotten our established rule about [SPECIFIC RULE].
As we discussed earlier, we [EXPLANATION].
Please revise your approach to follow this rule.
```

#### When Patterns Are Ignored
```
This doesn't follow the pattern we established for [SPECIFIC CONTEXT].
Please check [REFERENCE FILE] and use that pattern instead.
```

#### When Constraints Are Violated
```
CONSTRAINT VIOLATION: We agreed earlier that [CONSTRAINT].
Your current approach violates this constraint.
Please revise to ensure [SPECIFIC COMPLIANCE].
```

### Best Practices for Long Conversations

#### Create Persistent Documentation
Instead of relying on conversation memory, create files that persist:

```markdown
# SESSION_RULES.md
Rules established in current session:
1. [RULE WITH TIMESTAMP]
2. [RULE WITH TIMESTAMP]
3. [RULE WITH TIMESTAMP]

Last updated: [TIMESTAMP]
```

#### Use File-Based Instructions
Store complex instructions in files rather than repeating them:

```
Please read CURRENT_TASK.md for the complete requirements.
The context and constraints are documented there.
```

#### Checkpoint Files
Create progress files that can be referenced:

```markdown
# PROGRESS.md
## Completed
- [TASK 1] - Completed at [TIMESTAMP]
- [TASK 2] - Completed at [TIMESTAMP]

## Current Rules
- [ACTIVE RULE 1]
- [ACTIVE RULE 2]

## Next Steps
- [PLANNED TASK 1]
- [PLANNED TASK 2]
```

### Context Compacting Indicators

#### Behavioral Changes
- Asking about previously established conventions
- Suggesting approaches that were rejected earlier
- Creating files in wrong locations
- Using different naming patterns
- Ignoring test requirements

#### Response to Behavioral Changes
```
CONTEXT ALERT: You're behaving differently than earlier in our conversation.
Earlier we established [SPECIFIC RULE/PATTERN].
Please return to that approach.
```

### Emergency Context Reload Template
```
EMERGENCY CONTEXT RELOAD:

Project: [PROJECT NAME]
Language/Framework: [TECH STACK]

Critical Rules:
1. [MOST IMPORTANT RULE]
2. [SECOND MOST IMPORTANT]
3. [THIRD MOST IMPORTANT]

Current Task: [CURRENT TASK]
Constraints: [KEY CONSTRAINTS]

Files to Reference:
- [FILE 1] for [PURPOSE]
- [FILE 2] for [PURPOSE]

Please confirm understanding before continuing.
```

## Success Metrics

### Good Instruction Following
- Claude Code reads relevant files before making changes
- Follows established patterns and conventions
- Runs required validation steps (tests, linting, type checking)
- Uses existing utilities instead of creating duplicates
- Maintains backward compatibility

### Effective Communication
- Clear, specific prompts yield better results
- Well-documented projects get more consistent behavior  
- Regular corrections improve performance over time
- Context-rich instructions reduce back-and-forth

### Context Continuity
- Rules remain consistent throughout long conversations
- Project patterns are maintained despite context compacting
- Documentation files provide reliable reference points
- Emergency reload procedures restore proper behavior quickly

Remember: Claude Code learns from your instructions and feedback within each conversation, but context compacting can cause memory loss. Invest in persistent documentation and proactive context management to maintain productivity across long sessions.
