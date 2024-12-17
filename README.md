# Rules Server MCP

A Model Context Protocol (MCP) server that provides access to rules and categories.

## Features

- Get all rules or filter by category
- Get list of all rule categories

## Rules Storage

Rules are stored in two locations:
- Global rules: `~/Library/Application Support/Windsurf/User/globalStorage/rooveterinaryinc.roo-cline/settings/global_rules.md`
- Workspace rules: In your project directory as `workspace_rules.md`

These markdown files contain the rules in a structured format that the server parses and serves through its MCP tools.

## Installation

1. Clone or download this repository
2. Install dependencies:
```bash
npm install
```
3. Build the server:
```bash
npm run build
```

### Step-by-Step Installation Example

Here's a concrete example for a user named "hugo":

1. Create the MCP directory:
```bash
mkdir -p /Users/hugo/Documents/Cline/MCP
cd /Users/hugo/Documents/Cline/MCP
```

2. Clone the repository:
```bash
git clone https://github.com/bartwisch/MCPRules.git
cd rules-server
```

3. Install dependencies:
```bash
npm install
```

4. Build the server:
```bash
npm run build
```

5. Configure the MCP settings. For VSCode, edit:
```bash
vim /Users/hugo/Library/Application Support/Windsurf/User/globalStorage/rooveterinaryinc.roo-cline/settings/cline_mcp_settings.json
```

Add this configuration:
```json
{
  "mcpServers": {
    "rules": {
      "command": "node",
      "args": ["/Users/hugo/Documents/Cline/MCP/rules-server/build/index.js"],
      "disabled": false,
      "alwaysAllow": []
    }
  }
}
```

6. Create or ensure the rules files exist:
```bash
touch "/Users/hugo/Library/Application Support/Windsurf/User/globalStorage/rooveterinaryinc.roo-cline/settings/global_rules.md"
```

## Configuration

Add the rules-server to your MCP settings configuration file. The location depends on your environment:

### For Cline VSCode Extension
Location: `~/Library/Application Support/Windsurf/User/globalStorage/rooveterinaryinc.roo-cline/settings/cline_mcp_settings.json`

### For Claude Desktop App
Location: `~/Library/Application Support/Claude/claude_desktop_config.json`

Add the following configuration:

```json
{
  "mcpServers": {
    "rules": {
      "command": "node",
      "args": ["/path/to/rules-server/build/index.js"],
      "disabled": false,
      "alwaysAllow": []
    }
  }
}
```

Replace `/path/to/rules-server` with the actual path to your rules-server installation.

## Usage

Once configured, the rules-server provides two tools that can be used through the MCP protocol:

### 1. Get Rules

Retrieve all rules or filter by category:

```typescript
<use_mcp_tool>
<server_name>rules-server</server_name>
<tool_name>get_rules</tool_name>
<arguments>
{
  "category": "optional-category-name"
}
</arguments>
</use_mcp_tool>
```

### 2. Get Categories

Retrieve a list of all available rule categories:

```typescript
<use_mcp_tool>
<server_name>rules-server</server_name>
<tool_name>get_categories</tool_name>
<arguments>
{}
</arguments>
</use_mcp_tool>
```

## Development

To modify or extend the rules-server:

1. Source code is in the `src` directory
2. Make your changes
3. Rebuild using `npm run build`
4. Restart any applications using the MCP server to pick up the changes

## Error Handling

The server will return appropriate error messages if:
- Invalid category is provided
- Required parameters are missing
- Server encounters internal errors
- Rules files cannot be found or accessed

## License

MIT License