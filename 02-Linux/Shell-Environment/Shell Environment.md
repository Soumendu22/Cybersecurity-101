# Shell Environment

## Shell Fundamentals

A shell is a command interpreter that provides an interface to the OS.

Common shells:

- `bash`
- `zsh`
- `sh`

Check current shell:

```bash
echo "$SHELL"
ps -p $$
```

---

## Environment Variables

List environment:

```bash
env
printenv
```

Set temporary variable:

```bash
export TARGET=10.10.10.10
```

Use variable:

```bash
echo "$TARGET"
```

Security note: avoid storing secrets in shell history or plain environment values on shared systems.

---

## Shell Startup Files

For Bash, common files:

- `~/.bashrc` (interactive non-login)
- `~/.bash_profile` or `~/.profile` (login shell)
- `/etc/profile` (system-wide)

Apply updates:

```bash
source ~/.bashrc
```

---

## Aliases and Functions

Aliases:

```bash
alias ll='ls -lah'
alias ports='ss -tulnp'
```

Functions in `.bashrc`:

```bash
mkcd() {
  mkdir -p "$1" && cd "$1"
}
```

---

## PATH Management

View path:

```bash
echo "$PATH"
```

Add custom bin directory:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Security tips:

- avoid placing writable world directories in PATH
- prefer absolute paths in privileged scripts

---

## Command History

Useful commands:

```bash
history
history | tail -n 20
```

History config variables:

- `HISTSIZE`
- `HISTFILESIZE`
- `HISTCONTROL`

Reduce secret leakage:

```bash
export HISTCONTROL=ignoreboth
```

Prefix sensitive commands with a space if configured with `ignorespace`.

---

## Job Control and Session Management

```bash
jobs
fg
bg
nohup long_task.sh &
```

Terminal multiplexers:

- `tmux`
- `screen`

Useful for long-running recon and monitoring sessions.

---

## Prompt Customization

Prompt variable: `PS1`.

Example with user, host, cwd:

```bash
export PS1='\u@\h:\w\$ '
```

Security-friendly prompt ideas:

- show current git branch
- highlight root shell
- show exit status of previous command

---

## Useful Shell Productivity Tools

- reverse search: `Ctrl + R`
- command chaining: `&&`, `||`, `;`
- brace expansion: `{a,b,c}`
- xargs for bulk command execution

Examples:

```bash
cat hosts.txt | xargs -I{} ping -c 1 {}
```

---

## Practice Tasks

1. Build a secure `.bashrc` profile with aliases and helper functions.
2. Add a custom prompt that highlights root and non-zero exit codes.
3. Configure history behavior to minimize credential leakage.
4. Create reusable shell functions for recon workflows.
5. Audit PATH and remove risky entries.
