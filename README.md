# Gemini CLI Extension - MySQL

> [!NOTE]
> This extension is currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

This Gemini CLI extension provides a set of tools to interact with [MySQL](https://dev.mysql.com/doc/) instances. It allows you to manage your databases, execute queries, and explore schemas directly from the [Gemini CLI](https://google-gemini.github.io/gemini-cli/), using natural language prompts.
> [!IMPORTANT]
> **We Want Your Feedback!**
> Please share your thoughts with us by filling out our feedback [form][form]. 
> Your input is invaluable and helps us improve the project for everyone.

[form]: https://docs.google.com/forms/d/e/1FAIpQLSfEGmLR46iipyNTgwTmIDJqzkAwDPXxbocpXpUbHXydiN1RTw/viewform?usp=pp_url&entry.157487=mysql

## Why Use the MySQL Extension?

* **Natural Language Management:** Stop wrestling with complex commands. Explore schemas and query data by describing what you want in plain English.
* **Seamless Workflow:** As a Google-developed extension, it integrates seamlessly into the Gemini CLI environment. No need to constantly switch contexts for common database tasks.
* **Code Generation:** Accelerate development by asking Gemini to generate data classes and other code snippets based on your table schemas.


## Prerequisites

Before you begin, ensure you have the following:

* One of the supported agent harnesses, installed and authenticated:
  * [Gemini CLI](https://github.com/google-gemini/gemini-cli) (v0.6.0+)
  * [Claude Code](https://code.claude.com)
  * [Codex](https://developers.openai.com/codex) (v0.150.0+)
  * [Antigravity CLI](https://antigravity.google)
* [Node.js](https://nodejs.org/) (the MCP server runs via `npx`).
* A running MySQL instance.
* A user with database-level permissions to execute queries.

## Getting Started

### Installation

All harnesses use the same plugin; the MCP server runs via `npx` (no binary to download). Install with your harness of choice:

**Gemini CLI**

```bash
gemini extensions install https://github.com/gemini-cli-extensions/mysql
```

**Claude Code**

```bash
claude plugin marketplace add gemini-cli-extensions/mysql
claude plugin install mysql@mysql
```

**Codex**

```bash
codex plugin marketplace add gemini-cli-extensions/mysql
codex plugin add mysql@mysql
```

**Antigravity**

```bash
agy plugin install https://github.com/gemini-cli-extensions/mysql
```

See [Configuration](#configuration) for how each harness supplies the connection settings.

### Configuration

The plugin connects to MySQL using these settings:

*   `MYSQL_HOST`: (Optional) The MySQL host. Defaults to `localhost`.
*   `MYSQL_PORT`: (Optional) The MySQL port. Defaults to `3306`.
*   `MYSQL_DATABASE`: The name of the database to connect to.
*   `MYSQL_USER`: The database username.
*   `MYSQL_PASSWORD`: The password for the database user.

How you supply them depends on the harness:

*   **Gemini CLI**: prompted on install and saved to the extension's `.env`. View or update later with `gemini extensions list` / `gemini extensions config mysql [setting] [--scope user|workspace]` (restart the CLI to apply).
*   **Claude Code**: pass `--config KEY=VALUE` on install (repeatable), or run `/plugin` inside Claude Code.
*   **Codex** and **Antigravity**: export the variables in your shell before starting:

```bash
export MYSQL_HOST="<your-mysql-host>"       # Optional, defaults to localhost
export MYSQL_PORT="<your-mysql-port>"       # Optional, defaults to 3306
export MYSQL_DATABASE="<your-database-name>"
export MYSQL_USER="<your-database-user>"
export MYSQL_PASSWORD="<your-database-password>"
```

> [!NOTE]
> See [Troubleshooting](#troubleshooting) for debugging your configuration.

### Start Gemini CLI

To start the Gemini CLI, use the following command:

```bash
gemini
```

> [!WARNING]
> **Changing Instance & Database Connections**
> Currently, the database connection must be configured before starting the Gemini CLI and can not be changed during a session.
> To save and resume conversation history use command: `/chat save <tag>` and `/chat resume <tag>`.

## Usage Examples

Interact with MySQL using natural language right from your IDE:

* **Explore Schemas and Data:**
  * "Show me all tables in the 'orders' database."
  * "What are the columns in the 'products' table?"
  * "How many orders were placed in the last 30 days, and what were the top 5 most purchased items?"
* **Generate Code:**
  * "Generate a Python dataclass to represent the 'customers' table."

## Supported Tools

*  `list_tables`: Use this tool to list tables and descriptions.
*  `execute_sql`: Use this tool to execute any SQL statement.
*  `get_query_plan`: Use this tool to generate an execution plan.
*  `list_active_queries`: Use this tool to lists top N (default 10) ongoing queries.
*  `list_tables_missing_unique_indexes`: Use this tool to find tables that do not have primary or unique key constraint
*  `list_table_fragmentation`: Use this tool to list fragmented tables

## Additional Extensions

Find additional extensions to support your entire software development lifecycle at [github.com/gemini-cli-extensions](https://github.com/gemini-cli-extensions), including:
* [Cloud SQL for MySQL extension](https://github.com/gemini-cli-extensions/cloud-sql-mysql)
* and more!

## Troubleshooting

Use `gemini --debug` to enable debugging.

Common issues:

* "✖ Error during discovery for server: MCP error -32000: Connection closed": The database connection has not been established. Ensure your configuration is set via environment variables.
* "✖ MCP ERROR: Error: spawn npx ENOENT": Node.js/`npx` is not installed or not on your `PATH`. Install Node.js (which provides `npx`).
* "npm error"/network failures on first run: `npx` fetches `@toolbox-sdk/server` on first launch, so it needs network access. Retry once connectivity is available.
