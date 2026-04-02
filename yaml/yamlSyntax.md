# strings
## shell style parameter expansion
```yaml
llm:
    provider: "${LLM_PROVIDER:-openai_compatible}"
```
means use the env variable LLM_PROVIDER if set and non-empty,
else use default openai_compatible

if nothing after '-',
then just sub empty