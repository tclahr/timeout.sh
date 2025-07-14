# 🕒 timeout.sh - Lightweight Bash-Based Timeout Command

A fast and portable `timeout` command written in POSIX-compliant shell script. Perfect for systems where GNU `timeout` isn't available or when a minimal dependency solution is preferred.

## 🧭 Overview

The `timeout.sh` script allows you to run any command with a time limit. If the command exceeds the specified duration, it is terminated with a configurable signal (default: `SIGTERM`). It is a drop-in replacement for GNU `timeout`, fully implemented in shell script, making it ideal for minimal or embedded environments.

Whether you're scripting automated jobs, running system diagnostics, or managing CI/CD pipelines, `timeout` provides a simple yet powerful way to manage long-running commands.

## ✨ Features

- ✅ Fully written in POSIX shell (no external dependencies)
- ⏳ Accepts durations in seconds, minutes, hours, or days (`10`, `5m`, `2h`, `1d`)
- 🛑 Custom signal support: `--signal=SIGKILL`, `--signal=SIGTERM`, etc.
- 💣 Optional hard-kill after grace period via `--kill-after`
- 📦 Minimal and portable — great for Docker, initramfs, or restricted environments

## 🚀 Usage

```sh
timeout.sh [OPTIONS] DURATION COMMAND [ARGS]...
```

### Options

- `-s, --signal=SIGNAL` — Signal to send to command (default: `TERM`)
- `-k, --kill-after=DURATION` — Send `KILL` after this delay if command is still running
- `-h, --help` — Show help message

### Duration Formats

- `s` (seconds), `m` (minutes), `h` (hours), `d` (days)
- Default unit is seconds

### Exit Codes

- `124` — Command timed out
- `125` — Invalid usage or internal error
- `126` — Command found but cannot be executed
- `127` — Command not found
- Otherwise — Exit code of the command itself

### Examples

```sh
timeout.sh 10 sleep 5             # Success - finishes before timeout
timeout.sh 5 sleep 10             # Timeout - sleep killed after 5s
timeout.sh -s KILL 10 my_script   # Uses SIGKILL instead of SIGTERM
timeout.sh -k 2 10 long_task.sh   # Grace period before SIGKILL
```

## ⚙️ Requirements

- POSIX-compliant shell (e.g., `/bin/sh`)
- Basic Unix utilities: `expr`, `sed`, `which` or `command -v`

## 🤝 Contributing

Contributions are welcome! To propose enhancements or fixes:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request with a clear description

If you encounter bugs or have feature suggestions, please open an [issue](https://github.com/tclahr/timeout.sh/issues).

## 📜 License

This project is licensed under the **Apache 2.0 License** — see the [`LICENSE`](LICENSE) file for details.
