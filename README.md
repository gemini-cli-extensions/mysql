# Gemini CLI Extension - MySQL

This Gemini CLI extension provides a set of tools to interact with [MySQL](https://dev.mysql.com/doc/) instances. It allows you to manage your databases, execute queries, and explore schemas directly from the [Gemini CLI](https://google-gemini.github.io/gemini-cli/), using natural language prompts.

## Why Use the MySQL Extension?

* **Integrated with Gemini CLI:** As a Google-developed extension, it integrates seamlessly into the Gemini CLI environment, making security an accessible part of your workflow.
* **Connect to MySQL:** Securely connect to your MySQL instances.
* **Explore Database Schema:** List databases, tables, views, and schemas.
* **Query your Database:** Execute SQL queries against your database.

## Prerequisites

Before you begin, ensure you have the following:

* [Gemini CLI](https://github.com/google-gemini/gemini-cli) installed.
* A running MySQL instance.

## Installation

To install the extension, use the command:

```bash
gemini extensions install github.com/gemini-cli-extensions/mysql
```

## Configuration

* `MYSQL_HOST`: The hostname or IP address of the MySQL server.
* `MYSQL_PORT`: The port number of the MySQL server.
* `MYSQL_DATABASE`: The name of the database to connect to.
* `MYSQL_USER`: The username for authentication.
* `MYSQL_PASSWORD`: The password for authentication.

## Supported Tools

* `list_tables`
* `execute_sql`

## Additional Extensions

Find additional extensions to support your entire software development lifecycle at [github.com/gemini-cli-extensions](https://github.com/gemini-cli-extensions).

## Troubleshooting

* "cannot execute binary file": Ensure the correct binary for your OS/Architecture has been downloaded. See [Installing the server](https://googleapis.github.io/genai-toolbox/getting-started/introduction/#installing-the-server) for more information.
