# Kube-Admin-Scripts

## knslogs

### Overview

This script is designed to help you search and analyze Kubernetes pod logs using the ripgrep command-line tool. It compiles the results into a Markdown report, making it easy to share with team members or keep track of important log events. The script supports customizing the search pattern, output file, and additional ripgrep arguments for advanced usage.


### Usage

To use this script, simply run it with the desired options and arguments:


```bash
./knslogs.sh [--all|--error|--warn|--http] [--file filename.md] [--rg-args 'custom rg arguments'] <namespace>
```

Here's a breakdown of the available options and their meanings:



  --all: Use this option to search for all log events with the default search pattern (error|warn|fatal).

  --error, --warn, or --http (4XX|5XX): Specify one of these options to search for logs containing the specified keyword. For example, use --error to search for error messages.

  --file: Provide a filename (e.g., filename.md) to save the compiled Markdown report. If this option is not used, the script will display the results directly in the terminal.

  --rg-args: Pass any custom ripgrep arguments you want to use with the search command. For example, --rg-args '--ignore-case' would ignore case sensitivity during the search.

by defaut --all --error --warn and --http use the power of ripgrep to filter logs and providing context with the two line before the patern match and 3 line after the partern match

### Search Pattern Used

The script uses a default search pattern (error|warn|fatal) to filter log events. If you specify a custom search pattern using one of the options mentioned above, it will be displayed in the Markdown report along with any custom ripgrep arguments provided.


### Log Analysis and Results

For each pod in the specified namespace, the script will display or save the following information:

- Pod name and namespace

- Container names within the pod

- Search results (if a search pattern is specified) or full logs (if no search pattern is specified) for each container


### Example Usage

To search for error messages in all pods within the kube-system namespace and save the results to a file named error_logs.md, run the following command:


```bash
./knslogs.sh --error --file error_logs.md kube-system
```

If you use this script a lot :

```bash
mv knslogs.sh /usr/local/bin/knslogs
```

You can now run the script using ;
```bash
knslogs <namespace>
```
