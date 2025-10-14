# Gemini CLI Extension - MySQL

> [!NOTE]
> This extension is currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

This Gemini CLI extension provides a set of tools to interact with [MySQL](https://dev.mysql.com/doc/) instances. It allows you to manage your databases, execute queries, and explore schemas directly from the [Gemini CLI](https://google-gemini.github.io/gemini-cli/), using natural language prompts.

## Why Use the MySQL Extension?

* **Natural Language Management:** Stop wrestling with complex commands. Explore schemas and query data by describing what you want in plain English.
* **Seamless Workflow:** As a Google-developed extension, it integrates seamlessly into the Gemini CLI environment. No need to constantly switch contexts for common database tasks.
* **Code Generation:** Accelerate development by asking Gemini to generate data classes and other code snippets based on your table schemas.

## Prerequisites

Before you begin, ensure you have the following:

* [Gemini CLI](https://github.com/google-gemini/gemini-cli) installed with version **+v0.6.0**.
* A running MySQL instance.
* A user with database-level permissions to execute queries.

## Getting Started

### Installation

To install the extension, use the command:

```bash
gemini extensions install https://github.com/gemini-cli-extensions/mysql
```

### Configuration

Set the following environment variables before starting the Gemini CLI:

* `MYSQL_HOST`: The hostname or IP address of the MySQL server.
* `MYSQL_PORT`: The port number of the MySQL server.
* `MYSQL_DATABASE`: The name of the database to connect to.
* `MYSQL_USER`: The username for authentication.
* `MYSQL_PASSWORD`: The password for authentication.

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

* "failed to find default credentials: google: could not find default credentials.": Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment. See [Set up Application Default Credentials](https://cloud.google.com/docs/authentication/external/set-up-adc) for more information.
* "✖ Error during discovery for server: MCP error -32000: Connection closed": The database connection has not been established. Ensure your configuration is set via environment variables.
* "✖ MCP ERROR: Error: spawn /Users/USER/.gemini/extensions/mysql/toolbox ENOENT": The Toolbox binary did not download correctly. Ensure you are using Gemini CLI v0.6.0+.
* "cannot execute binary file": The Toolbox binary did not download correctly. Ensure the correct binary for your OS/Architecture has been downloaded. See [Installing the server](https://googleapis.github.io/genai-toolbox/getting-started/introduction/#installing-the-server) for more information.