# Kubernetes Log Search and Report Script

This repository contains a script designed to simplify the process of searching through Kubernetes pod logs and compiling the results into a Markdown report as an option. It leverages `kubectl` and `rg` (ripgrep) to efficiently search logs for specified patterns.

## Features

- **Flexible Log Level Filtering:** Search for logs by different levels (error, warn, http) or by custom search patterns.
- **Markdown Report Generation:** Compile the search results into a neatly formatted Markdown file.
- **Custom `rg` Arguments:** Advanced users can pass custom arguments to `rg` for more granular control over the search.

## Prerequisites

Before using this script, ensure you have the following installed:
- `kubectl`: The command-line tool for interacting with Kubernetes clusters.
- `rg` (ripgrep): A line-oriented search tool that recursively searches your current directory for a regex pattern.

## Usage

```bash
./log_search_script.sh [options] <namespace>
```

## Options
-a, --all: Use the default search pattern (error, warn, fatal).
-e, --error: Search for logs with the 'error' level.
-w, --warn: Search for logs with the 'warn' level.
-h, --http: Search for logs with HTTP status codes like 404, 403, etc.
-f, --file <filename.md>: Specify the Markdown file to output the report.
-s, --search <pattern>: Use a custom search pattern.
--rg-args '<args>': Provide custom ripgrep arguments for the search.

## Examples
```bash
./knslogs.sh --error --file error_report.md my_namespace
./knslogs.sh --all --rg-args '--ignore-case --follow' my_namespace
./knslogs.sh -s 'custom pattern or regex' my_namespace
```

## How It Works
The script first checks for the provided namespace and required options.
Based on the specified options, it constructs a search pattern.

It then iterates over all pods in the given namespace, retrieving logs for each container.
The logs are searched for the specified pattern using rg, and the results are optionally written to the specified Markdown file.

## Contributing
Contributions are welcome! If you'd like to improve this script or add features, please fork the repository and submit a pull request.
