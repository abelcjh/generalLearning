# alternative to claude code
when use different models for architect and editor

set up
```bash
aider
      --architect
      --model gmi/claude-4.7-opus
      --editor-model gmi/qwen-3.5-max
      --no-auto-accept-architect
```

when no auto accept, aider will ask you want to proceed with plan or not,
then can give more prompts, architect rewrite plan then only pass to editor

can also toggle this off
```bash
/auto-accept-architect off
```

2026 only aider natively supports architect editor split via cli, without manual ui switching