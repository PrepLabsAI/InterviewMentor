# Use with Claude Code

Claude Code provides the most integrated experience — skills load natively and the interviewer persona persists throughout the session.

## Prerequisites

- [Claude Code](https://claude.ai/code) installed

## Install

In Claude Code, run:

```
/plugin marketplace add PrepLabsAI/InterviewMentor
/plugin install coding-interview-agent@coding-interview-preparation-agents-marketplace
```

This installs all 44 interviewers. Restart Claude Code if the skills don't show up right away.

To pick up new interviewers later:

```
/plugin marketplace update coding-interview-preparation-agents-marketplace
```

## Start an interview

Ask for a topic in plain language, or name a specific interviewer:

```
> "Help me prepare for a system design interview."
> "Use the uber-interviewer skill and start my mock interview."
> "Use the arrays-hashmaps-interviewer skill and interview me."
> "Use the dynamic-programming-interviewer skill."
```

See the [Roster](../README.md#-roster) for every interviewer name.

## What to expect

Once loaded, the interviewer will:
1. Greet you and immediately start with a warm-up question
2. Adapt difficulty based on your answers
3. Provide hints when you ask (4 levels of progressively detailed help)
4. Generate a scorecard at the end with specific improvement areas

## Tips

- **Say the exact skill name** (e.g., "uber-interviewer") so Claude picks the right one.
- **Ask for hints** naturally: "Can I get a hint?" or "I'm stuck, help me."
- **Request the scorecard** at the end: "Give me my evaluation."

## Alternative: Install from a local clone

If you're editing skills and want to try your changes, install from your clone instead of GitHub:

```bash
git clone https://github.com/PrepLabsAI/InterviewMentor.git
```

Then in Claude Code:

```
/plugin marketplace add ./InterviewMentor
/plugin install coding-interview-agent@coding-interview-preparation-agents-marketplace
```

After editing a skill, run `/plugin marketplace update coding-interview-preparation-agents-marketplace` and restart Claude Code to load the change.
