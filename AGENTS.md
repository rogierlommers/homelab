# Agent Instructions

Before starting to work, dynamically discover and read every Markdown rule file in
`.agent/`. Use this command to get the full set of rules:

```bash
find .agent -type f -name "*.md" | sort
```

Read and follow every file returned by that command. These rules are always-on for this repository and must be treated as required.
