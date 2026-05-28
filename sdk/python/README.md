# OpenAI Codex Python SDK (Beta)

Experimental Python SDK for `codex-general app-server` JSON-RPC v2 over stdio, with a small default surface optimized for real scripts and apps.

The generated wire-model layer is sourced from the pinned `openai-codex-cli-bin`
runtime package and exposed as Pydantic models with snake_case Python fields
that serialize back to the app-server’s camelCase wire format.
The package root exports the ergonomic client API; public app-server value and
event types live in `openai_codex.types`.
Build Python applications that start Codex General threads, run turns, stream progress,
and control workspace access.

## Install

Install the SDK:

```bash
pip install openai-codex
```

## Quickstart

The SDK reuses your existing Codex authentication when one is already
available:

```python
from openai_codex import Codex

with Codex() as codex:
    thread = codex.thread_start()
    result = thread.run("Explain this repository in three bullets.")
    print(result.final_response)
```

`thread.run(...)` returns a `TurnResult` containing the final response,
collected items, and token usage.

## Authentication

Existing Codex authentication is reused automatically. To start ChatGPT
browser login explicitly:

```python
from openai_codex import Codex

with Codex() as codex:
    login = codex.login_chatgpt()
    print(login.auth_url)
    print(login.wait().success)
```

For device-code login:

```python
with Codex() as codex:
    login = codex.login_chatgpt_device_code()
    print(login.verification_url, login.user_code)
    login.wait()
```

For API-key login:

```python
with Codex() as codex:
    codex.login_api_key("sk-...")
```

## Built-In Help

Use Python's standard `help(openai_codex)`, `help(Codex)`, or
`python -m pydoc openai_codex` documentation tools.

## Documentation

- [Getting started](https://github.com/timwhitez/codex-general/blob/main/sdk/python/docs/getting-started.md)
- [API reference](https://github.com/timwhitez/codex-general/blob/main/sdk/python/docs/api-reference.md)
- [FAQ](https://github.com/timwhitez/codex-general/blob/main/sdk/python/docs/faq.md)
- [Examples](https://github.com/timwhitez/codex-general/blob/main/sdk/python/examples/README.md)

The package is licensed under the
[repository Apache License 2.0](https://github.com/timwhitez/codex-general/blob/main/LICENSE).
