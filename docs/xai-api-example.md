# Use Magic Hour with the xAI API

Add the Magic Hour MCP server to a Grok request as a remote MCP tool.

```python
import os
from openai import OpenAI

client = OpenAI(api_key=os.getenv("XAI_API_KEY"), base_url="https://api.x.ai/v1")

response = client.responses.create(
    model="grok-4.7",  # use any current Grok model
    input=[{"role": "user", "content": "Create an image of a red bicycle on a beach at sunset."}],
    tools=[{
        "type": "mcp",
        "server_url": "https://mcp.magichour.ai/",
        "server_label": "magic_hour",
        "server_description": "Create and edit images and video with Magic Hour",
        "authorization": os.getenv("MAGIC_HOUR_API_KEY"),
        # Optional: expose only the tools you need.
        # "allowed_tools": ["ai_image_generator_create_image", "wait_for_image_project"],
    }],
)
print(response)
```

Notes
- Create an API key in the Magic Hour Developer Hub and keep it in an environment variable.
- If the request is rejected as unauthorized, try `"Bearer <key>"` as the `authorization` value. (Untested: confirm which form xAI sends.)
- Creation tools are asynchronous. The model should call the matching `wait_for_*_project` tool until the project finishes.
- Generations spend Magic Hour credits.
