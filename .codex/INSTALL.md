# Installing Mailgo Campaign Suite for Codex

Enable Mailgo campaign skills in Codex via native skill discovery. Just clone and symlink.

## Prerequisites

- Git
- Python 3.7+

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/leadsnaviDeveloper/mailgo-cold-mail-marketing.git ~/.codex/mailgo-campaign-suite
   ```

2. **Create the skills symlink:**
   ```bash
   mkdir -p ~/.agents/skills
   ln -s ~/.codex/mailgo-campaign-suite/skills ~/.agents/skills/mailgo-campaign-suite
   ```

   **Windows (PowerShell):**
   ```powershell
   New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills"
   cmd /c mklink /J "$env:USERPROFILE\.agents\skills\mailgo-campaign-suite" "$env:USERPROFILE\.codex\mailgo-campaign-suite\skills"
   ```

3. **Set your API key:**
   ```bash
   # macOS / Linux
   echo 'export MAILGO_API_KEY="YOUR_TOKEN"' >> ~/.zshrc && source ~/.zshrc

   # Windows PowerShell
   [System.Environment]::SetEnvironmentVariable('MAILGO_API_KEY', 'YOUR_TOKEN', 'User')
   ```

   Get your token from [app.mailgo.ai](https://app.mailgo.ai) → Avatar → Personal Tokens → Create Token.

4. **Restart Codex** to discover the skills.

## Verify

```bash
ls -la ~/.agents/skills/mailgo-campaign-suite
```

You should see a symlink pointing to your mailgo-campaign-suite skills directory.

## Updating

```bash
cd ~/.codex/mailgo-campaign-suite && git pull
```

Skills update instantly through the symlink.

## Uninstalling

```bash
rm ~/.agents/skills/mailgo-campaign-suite
rm -rf ~/.codex/mailgo-campaign-suite
```
