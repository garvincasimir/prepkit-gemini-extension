# PrepKit for Gemini CLI

Install with Gemini CLI:

```sh
gemini extensions install https://github.com/garvincasimir/prepkit-gemini-extension
```

Review the extension permissions, then use `/mcp auth prepkit` in Gemini CLI when authentication is requested. This extension targets Gemini CLI; it does not add a connector to the Gemini consumer chat app.

This package connects an assistant to the PrepKit MCP server at `https://mcp.prepkit.cazimedia.com/mcp`. Your assistant supplies inference through its own account, plan and usage limits. PrepKit does not receive its password or API key.

Sign in to PrepKit when the assistant requests a connection. Review the permissions before approving. Ask your assistant to read `get_kitml_contract`; it returns the complete text-only source schema and a working example. Content submission requires a learner-created upload grant. Submitted kits wait for your review in PrepKit before joining your library.

Text-only assistants can call `validate_kitml_source` and `submit_private_kit_source`. Media packages use the KitML ZIP tools.

To revoke access, open PrepKit, choose **My PrepKits**, then **Create or import**, and disconnect the assistant in the connected list.
