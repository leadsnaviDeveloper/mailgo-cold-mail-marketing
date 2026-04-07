# Installing Mailgo Campaign Suite for OpenCode

## Prerequisites

- [OpenCode.ai](https://opencode.ai) installed
- Python 3.7+

## Installation

Add mailgo-campaign-suite to the `plugin` array in your `opencode.json` (global or project-level):

```json
{
  "plugin": ["mailgo-campaign-suite@git+https://github.com/leadsnaviDeveloper/mailgo-cold-mail-marketing.git"]
}
```

Restart OpenCode. The plugin auto-installs and registers all skills.

## Set your API key

```bash
# macOS / Linux
echo 'export MAILGO_API_KEY="YOUR_TOKEN"' >> ~/.zshrc && source ~/.zshrc

# Windows PowerShell
[System.Environment]::SetEnvironmentVariable('MAILGO_API_KEY', 'YOUR_TOKEN', 'User')
```

Get your token from [app.mailgo.ai](https://app.mailgo.ai) → Avatar → Personal Tokens → Create Token.

## Verify

Ask OpenCode: "Tell me about mailgo campaign suite"

Or use the native `skill` tool:

```
use skill tool to list skills
use skill tool to load mailgo-campaign-suite
```

## Updating

Updates automatically when you restart OpenCode.

To pin a specific version:

```json
{
  "plugin": ["mailgo-campaign-suite@git+https://github.com/leadsnaviDeveloper/mailgo-cold-mail-marketing.git#v1.0.0"]
}
```

## Troubleshooting

### Plugin not loading

1. Check logs: `opencode run --print-logs "hello" 2>&1 | grep -i mailgo`
2. Verify the plugin line in your `opencode.json`
3. Make sure you're running a recent version of OpenCode

### Skills not found

1. Use `skill` tool to list what's discovered
2. Check that the plugin is loading (see above)

## Getting Help

- Report issues: https://github.com/leadsnaviDeveloper/mailgo-cold-mail-marketing/issues
- Product: https://app.mailgo.ai
