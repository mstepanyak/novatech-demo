# NovaTech Solutions

Demo project for the **Advanced Claude Code** course on Pluralsight.

## Quick Start

### 1. Clone the Repository
```bash
# Clone the repository
git clone https://github.com/nyisztor/novatech-demo.git
cd novatech-demo

# Install dependencies
npm install
```

### 2. Figma Designs (Optional)

For the Figma MCP integration modules, you can duplicate the NovaTech designs to your own Figma account:

**Figma Design File:**  
[https://www.figma.com/design/UZ2t3sc5vi2cn9MXHkOfLY/NovaTech-Solutions?node-id=1-2&p=f](https://www.figma.com/design/UZ2t3sc5vi2cn9MXHkOfLY/NovaTech-Solutions?node-id=1-2&p=f)

**To use:**
- Click the link (requires free Figma account)
- The design file opens in Figma
- You can inspect, use with MCP, or duplicate to your Drafts if you want your own editable copy

**What's included:**
- Homepage (current design)
- Homepage - Updated (with design changes for demos)

**Note:** This is optional. You can follow along with the videos without opening the file, or practice MCP integration with your own Figma files.

### 3. Setting Up API Tokens

To use the GitHub MCP server, you'll need to configure an API token as an environment variable. This keeps your credentials secure and out of version control. The Figma MCP server doesn't need a token — see [3.2](#32-figma-access-no-token-needed).

#### 3.1 GitHub Token

**Create a token:**
1. Go to https://github.com/settings/tokens
2. Click "Generate new token" → "Generate new token (classic)"
3. Give it a name like "Claude Code MCP"
4. Select scopes: `repo` (for private repos) and `read:org` (for organization access)
5. Click "Generate token" and copy it

**Set the environment variable:**

**macOS (zsh):**
```bash
echo 'export GITHUB_TOKEN=your_token_here' >> ~/.zshrc
source ~/.zshrc
```
*Note: macOS uses zsh as the default shell*

**Linux (bash):**
```bash
echo 'export GITHUB_TOKEN=your_token_here' >> ~/.bashrc
source ~/.bashrc
```
*Note: Most Linux systems use bash as the default shell*

**Windows (PowerShell/Command Prompt):**
```cmd
setx GITHUB_TOKEN "your_token_here"
```
Then restart your terminal.

*Alternative:* You can also set it through System Properties → Environment Variables → New User variable

#### 3.2 Figma Access (No Token Needed)

The `figma-remote` server configured in `.mcp.json` connects to Figma's hosted remote MCP endpoint (`https://mcp.figma.com/mcp`) and authenticates via **OAuth**. The first time Claude Code uses a Figma tool, it opens a browser window for you to sign in — no personal access token is required.

**Verify the GitHub token is set:**
```bash
echo $GITHUB_TOKEN
```

From this point on, `GITHUB_TOKEN` will be available in every new terminal session, and Claude Code will pick it up automatically when it starts.

**Alternative: token-based Figma configuration.** If you prefer connecting to Figma with a personal access token (e.g., using `X-Figma-Token` headers) instead of OAuth, see `.mcp.example.json` for a sample configuration. This isn't the setup used by this project's `.mcp.json`, but you can adapt it if needed.


### 4. Verify Setup

```bash
# Open the website
npm run dev
```

Open: **http://localhost:3000/pages/index.html**

```bash
# In another terminal, launch Claude Code
claude
```
---

## ⚠️ Important: View Hidden Files

This project uses a `.claude/` folder for Claude Code configurations. This folder is **hidden by default** on most operating systems.

**To see hidden files:**

| OS | Method |
|----|--------|
| **macOS** | In Finder: Press `Cmd + Shift + .` |
| **Windows** | In File Explorer: View → Show → Hidden items |
| **VS Code** | Hidden files are visible by default |
| **Linux** | In file manager: `Ctrl + H` or View → Show Hidden Files |
| **Terminal** | Use `ls -la` instead of `ls` |

The `.claude/` folder contains subagents, skills, hooks, and enterprise templates used throughout this course.

## About This Project

NovaTech Solutions is a fictional tech consultancy website. It serves as a hands-on learning environment for advanced Claude Code features:

| Module | Feature | Key Files |
|--------|---------|-----------|
| 1 | MCP Server Integration | `.mcp.json` |
| 2 | Subagents | `.claude/agents/` |
| 3 | Git Worktrees | `scripts/setup-worktrees.sh` |
| 4 | Enterprise Features | `.claude/enterprise-templates/` |
| 5 | Agent Skills | `.claude/skills/` |
| 6 | Hooks | `.claude/settings.json` |

## Project Structure

```
novatech-demo/
├── src/
│   ├── pages/          # HTML pages: index, services, portfolio, team, contact
│   ├── css/            # base.css, components.css, variables.css, pages/*.css
│   └── js/             # navigation.js, contact-form.js, validation.js, portfolio-filters.js
├── tests/
│   ├── e2e/            # Playwright tests (contact-form.spec.js, navigation.spec.js)
│   └── unit/           # Node.js unit tests (validation.test.js)
├── docs/
│   ├── api-spec.md     # Backend API spec (planned; site currently simulates it client-side)
│   └── figma-spec.md   # Design tokens: colors, typography, spacing, components
├── scripts/            # setup-worktrees.sh (Git Worktrees automation)
├── .claude/
│   ├── agents/            # Subagent definitions
│   ├── skills/            # Custom skills (code-review, code-documentation, accessibility-checker, form-validator)
│   ├── rules/             # Project-specific rules (e.g., api-docs.md)
│   ├── enterprise-templates/
│   ├── logs/              # Hook output logs (created at runtime)
│   └── settings.json      # Hooks and permissions configuration
├── .mcp.json              # MCP server configuration (GitHub, Figma remote)
├── .mcp.example.json      # Alternate MCP example (token-based Figma, filesystem server)
└── CLAUDE.md              # Project context
```

## Available Commands

Run these from the project root (`novatech-demo/`):

```bash
npm run dev            # Start local server (serves src/ at http://localhost:3000)
npm run lint           # Run ESLint on src/js/
npm run lint:fix       # Run ESLint and auto-fix issues
npm run format         # Run Prettier on src/**/*.{html,css,js}
npm run format:check   # Check formatting without writing changes
npm run test           # Run all tests (unit + e2e)
npm run test:unit      # Run Node.js unit tests (tests/unit/)
npm run test:e2e       # Run Playwright E2E tests (tests/e2e/)
npm run test:e2e:ui    # Run Playwright E2E tests in UI mode
```

See [`docs/api-spec.md`](docs/api-spec.md) for the (planned) backend API and [`docs/figma-spec.md`](docs/figma-spec.md) for design tokens (colors, typography, spacing, components).

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- Node.js 18+
- Git
- GitHub account (for MCP integration)

## Pre-configured Branches

The repository includes branches for the Git Worktrees module:

- `feature/services-redesign` — Services page layout updates
- `feature/contact-form` — Form validation improvements  
- `bugfix/responsive-nav` — Mobile navigation fixes

## Open Pull Requests

Two PRs are available for the MCP/GitHub integration demo:

- **PR #1**: Add client testimonials section
- **PR #2**: Update team page with new hires

## License

Educational project for Pluralsight. All rights reserved.
