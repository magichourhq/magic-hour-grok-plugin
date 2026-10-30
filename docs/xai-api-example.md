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
- Pass the raw Magic Hour API key as `authorization`. The [official xAI cookbook](https://github.com/xai-org/xai-cookbook/blob/002788b1fe838295a5e0b6adedcc8c216f807926/examples/database-over-mcp/README.md#how-it-works) documents that xAI sends it in a Bearer Authorization header. Do not add a second `Bearer` prefix.
- This example has not been executed against the xAI API. Source-confirmed header behavior is separate from actual authentication, generation and output verification. A read-only workflow through the xAI API still uses billed xAI inference.
- Creation tools are asynchronous. The model should call the matching `wait_for_*_project` tool until the project finishes.
- Generations spend Magic Hour credits.
