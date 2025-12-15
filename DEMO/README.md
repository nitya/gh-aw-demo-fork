# AI Native Dev Meetup

Let's stage an AZD template to play with.

```bash
mkdir DEMO
mkdir ai-agents-template
cd ai-agents-template
azd init -t get-started-with-ai-agents
...

```

---

## 1. Setup: GitHub Agentic Workflows

GitHub CLI extensions are repositories that provide additional gh commands.The name of the extension repository must start with `gh-` and it must contain an
executable of the same name. All arguments passed to the `gh <extname>` invocation
will be forwarded to the `gh-<extname>` executable of the extension.

**This command installs added GitHub CLI commands from the [https://github.com/githubnext/gh-aw](https://github.com/githubnext/gh-aw) Agentic Workflows repo.

```bash
gh extension install githubnext/gh-aw
✓ Installed extension githubnext/gh-aw
```

You can now explore the new commands:

```bash
gh aw --help
```

Agentic Workflows Commands:

```bash

GitHub Agentic Workflows from GitHub Next

Common Tasks:
  gh aw init                  # Set up a new repository
  gh aw new my-workflow       # Create your first workflow
  gh aw compile               # Compile all workflows
  gh aw run my-workflow       # Execute a workflow
  gh aw logs my-workflow      # View execution logs
  gh aw audit <run-id>        # Debug a failed run

For detailed help on any command, use:
  gh aw [command] --help

Usage:
  gh aw [flags]
  gh [command]

Setup Commands:
  add         Add agentic workflows from repositories to .github/workflows
  init        Initialize repository for agentic workflows
  new         Create a new workflow Markdown file with example configuration
  remove      Remove agentic workflow files matching the given name prefix
  secret      Manage repository secrets
  tokens      Inspect and bootstrap GitHub tokens for gh-aw
  update      Update agentic workflows from their source repositories and check for gh-aw updates

Development Commands:
  compile     Compile agentic workflow Markdown to GitHub Actions YAML
  fix         Apply automatic codemod-style fixes to agentic workflow files
  mcp         Manage MCP (Model Context Protocol) servers
  mcp-server  Run an MCP (Model Context Protocol) server exposing gh-aw commands as tools
  status      Show status of agentic workflows

Execution Commands:
  disable     Disable agentic workflows and cancel any in-progress runs
  enable      Enable agentic workflows
  run         Run one or more agentic workflows on GitHub Actions
  trial       Trial one or more agentic workflows as if they were running in a repository

Analysis Commands:
  audit       Investigate a single GitHub Actions workflow run and generate a concise report
  campaign    Inspect first-class campaign definitions from .github/workflows/*.campaign.md
  logs        Download and analyze agentic workflow logs with aggregated metrics

Utilities:
  pr          Pull request utilities

Additional Commands:
  help        Help about any command
  version     Show gh aw extension version information

Flags:
      --banner    Display ASCII logo banner with purple GitHub color theme
  -h, --help      help for gh
  -v, --verbose   Enable verbose output showing detailed information
      --version   version for gh

Use "gh [command] --help" for more information about a command.
```

---


## 2. Setup: GitHub Copilot CLI

Installed as part of dev container - run it with the command below:

```bash
copilot --help
```

Command help:

```bash

GitHub Copilot CLI - An AI-powered coding assistant

Options:
  --add-dir <directory>               Add a directory to the allowed list for file access (can be used multiple times)
  --additional-mcp-config <json>      Additional MCP servers configuration as JSON string or file path (prefix with @) (can be used multiple times; augments config from ~/.copilot/mcp-config.json for this
                                      session)
  --agent <agent>                     Specify a custom agent to use, only in prompt mode
  --allow-all-paths                   Disable file path verification and allow access to any path
  --allow-all-tools                   Allow all tools to run automatically without confirmation; required for non-interactive mode (env: COPILOT_ALLOW_ALL)
  --allow-tool [tools...]             Allow specific tools
  --banner                            Show the startup banner
  --continue                          Resume the most recent session
  --deny-tool [tools...]              Deny specific tools, takes precedence over --allow-tool or --allow-all-tools
  --disable-builtin-mcps              Disable all built-in MCP servers (currently: github-mcp-server)
  --disable-mcp-server <server-name>  Disable a specific MCP server (can be used multiple times)
  --disable-parallel-tools-execution  Disable parallel execution of tools (LLM can still make parallel tool calls, but they will be executed sequentially)
  --disallow-temp-dir                 Prevent automatic access to the system temporary directory
  --enable-all-github-mcp-tools       Enable all GitHub MCP server tools instead of the default CLI subset
  -h, --help                          display help for command
  -i, --interactive <prompt>          Start interactive mode and automatically execute this prompt
  --log-dir <directory>               Set log file directory (default: ~/.copilot/logs/)
  --log-level <level>                 Set the log level (choices: "none", "error", "warning", "info", "debug", "all", "default")
  --model <model>                     Set the AI model to use (choices: "claude-sonnet-4.5", "claude-haiku-4.5", "claude-opus-4.5", "claude-sonnet-4", "gpt-5.1-codex-max", "gpt-5.1-codex", "gpt-5.2",
                                      "gpt-5.1", "gpt-5", "gpt-5.1-codex-mini", "gpt-5-mini", "gpt-4.1", "gemini-3-pro-preview")
  --no-color                          Disable all color output
  --no-custom-instructions            Disable loading of custom instructions from AGENTS.md and related files
  -p, --prompt <text>                 Execute a prompt in non-interactive mode (exits after completion)
  --resume [sessionId]                Resume from a previous session (optionally specify session ID)
  -s, --silent                        Output only the agent response (no stats), useful for scripting with -p
  --screen-reader                     Enable screen reader optimizations
  --stream <mode>                     Enable or disable streaming mode (choices: "on", "off")
  -v, --version                       show version information

Commands:
  help [topic]                        Display help information

Help Topics:
  config       Configuration Settings
  commands     Interactive Mode Commands
  environment  Environment Variables
  logging      Logging
  permissions  Tool Permissions

Examples:
  # Start interactive mode
  $ copilot

  # Start interactive mode and automatically execute a prompt
  $ copilot -i "Fix the bug in main.js"

  # Execute a prompt in non-interactive mode (exits after completion)
  $ copilot -p "Fix the bug in main.js" --allow-all-tools

  # Start with a specific model
  $ copilot --model gpt-5

  # Resume the most recent session
  $ copilot --continue

  # Resume a previous session using session picker
  $ copilot --resume

  # Resume with auto-approval
  $ copilot --allow-all-tools --resume

  # Allow access to additional directory
  $ copilot --add-dir /home/user/projects

  # Allow multiple directories
  $ copilot --add-dir ~/workspace --add-dir /tmp

  # Disable path verification (allow access to any path)
  $ copilot --allow-all-paths

  # Allow all git commands except git push
  $ copilot --allow-tool 'shell(git:*)' --deny-tool 'shell(git push)'

  # Allow all file editing
  $ copilot --allow-tool 'write'

  # Allow all but one specific tool from MCP server with name "MyMCP"
  $ copilot --deny-tool 'MyMCP(denied_tool)' --allow-tool 'MyMCP'
```


## 3. Run GitHub Copilot CLI & Activate Designer

```bash
copilot --banner
```

Activate the designer

```bash
> activate @.github/prompts/create-agentic-workflow.prompt.md
```

## 4. Run an Agentic Workflow

```bash
 > Generate a DEMO/docs folder with documentation for the DEMO/ai-agents-template and keep documentation up to date with changes 
 ```


Demo Ready