# openai_compatible
common name for a client mode
to call llm api providers
use http api
url and request follow openai compatible shape
path like `/v1/chat/completions`
so if no LLM_PROVIDER, use a provider that follow openai shape

action ➡️ adapter ➡️ client
http api, always has request and response

# adapters
before call llm api
map openclaw action to http api shape
depends on model provider
request, and parse the response given back

# client
adapter uses client, which is the code that calls the llm api, to send http api request
ie http/sdk client