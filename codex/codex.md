# use of different models
cant use non openai models in codex cli, but technically can route to gmi api cuz openai compatible
use agent loop heavily optimized for openai specific tool calling and computer use system prompts

but cant have different models for architect editor split

# cost
pay as you go
standard api

just one api key, used to identify account

# how to use
first in the repo root, run
```bash
codex /init
```

this will generate AGENTS.md file in repo, contain system prompt and memory for the agent
in this file, add architecture rules, formatting conventions, testing requirements

# to launch
```bash
codex
```

by default boot gpt-5.3.codex
ask for preferred permission level, auto read only or full access
auto safest, ask permission before run terminal command, or modify file outside working directory

# use openai models
can change model
```bash
/model gpt-5.4-codex
```

# how to control codex workflow
run
```bash
/plan
```
toggles to plan mode

```bash
/status
```
display current config,
and token usage

# add !
before prompts to turn them into bash commands