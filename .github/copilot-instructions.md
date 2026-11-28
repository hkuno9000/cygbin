# Copilot instructions for cygbin

## Repository purpose and architecture

This repository is a personal `~/bin` collection intended to work on Cygwin,
Git for Windows/MSYS2, WSL, Linux, and macOS. It contains public shell and
Perl utilities plus versioned configuration templates; private `*.sh` scripts
are intentionally ignored by `.gitignore`.

The setup flow is:

1. `myinit` is the bootstrap script. It creates home-directory backup/log
   directories, optionally configures the host, installs baseline packages on
   apt-based systems, clones this repository as `~/bin`, and invokes the
   remaining setup scripts.
2. `initmyrc` links repository configuration files such as `myvimrc`,
   `mytigrc`, `mycommit_template`, `myignore`, and `myeditorconfig` into `~`.
   Existing `.gitignore_global` and `.editorconfig` files are preserved.
3. `initbashrc` appends an interactive Bash configuration block to
   `~/.bashrc`; it does not replace the file. `myaliases` and `myfunctions`
   provide optional aliases and functions to source from an interactive shell.
4. The other executable files are standalone utilities. Notable groups are
   backup/diff tools (`backcp`, `backdiff`, `backrenumber`), repository/system
   helpers (`pullall`, `git-set-file-times`, `eachpath`), and interactive shell
   helpers (`killselect`, `ssh-list`, `nestgrep`).

Many scripts modify the home directory or system configuration and assume an
interactive Unix-like environment. Read the script and its `usage` output
before running it; several commands can use `sudo`, `apt`, `systemctl`, or
Windows path conventions.

## Build, test, and lint

There is no build system, package manifest, automated test suite, or configured
linter in this repository. Validate changes with the language-native syntax
checks from the repository root:

```sh
# Bash scripts
for f in backcp backdiff backrenumber colorcheck diffbash diffmy initbashrc \
  initmyrc killselect mygitconf myinit mysetting myupdate pi2wakepc.sh \
  pullall savehome; do bash -n "$f"; done

# POSIX shell scripts
sh -n bonsai.sh mysetting myupdate mysysinfo skykiso-web.sh ssh-list

# Perl scripts
perl -c headtail
perl -c eachpath
perl -c nestgrep
perl -c printpath
perl -c git-set-file-times
```

Use the relevant interpreter check for the file being changed. For behavior
that depends on a host, exercise a safe `--help`/usage path where available;
do not run setup or destructive commands merely as a test. There is no
single-test command because no test framework is present.

## Code and configuration conventions

- Preserve the existing shebang and interpreter boundary. Bash-specific
  features are used in Bash scripts; scripts marked `sh` should remain
  portable POSIX shell where practical; Perl utilities use direct executable
  shebangs.
- Follow `.editorconfig`: four-space tabs are the default, but `*.sh` uses
  two spaces. Existing files also use Vim modelines, which can clarify the
  intended indentation for a script.
- Keep scripts usable across Cygwin/MSYS2, WSL, Linux, and macOS. Existing
  code detects platform facilities such as `sudo`, Windows home paths, and
  `apt`; extend those patterns instead of assuming one host.
- Interactive confirmations conventionally go through `yesno`; the `-c`
  variant runs a command only after confirmation and preserves the command
  status. Avoid turning setup scripts into unattended destructive operations.
- Backup utilities intentionally use `cp --backup=t` naming and compare files
  before copying where appropriate. Preserve their existing backup search and
  diff conventions when adding related functionality.
- Configuration scripts are additive or link-based. In particular, do not
  overwrite user dotfiles when the existing script checks for and preserves
  them, and keep generated host-specific/private material out of tracked files.
- Shell aliases/functions are meant to be sourced into an interactive Bash
  session, not executed as standalone programs. Keep command names and
  cross-platform fallbacks consistent with `myaliases` and `myfunctions`.

## Repository guidance

`AGENTS.md` is authoritative for commits: do not create a commit unless the
user explicitly asks. Commit subjects start with the prescribed English
prefix (for example `Fix:`, `Feat:`, or `Docs:`), followed by the applicable
issue/feature/file context and summary; the body is Japanese with the required
problem/cause/fix or purpose/overview headings, wrapped to 80–120 columns.
