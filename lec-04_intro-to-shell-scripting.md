Shell scripting:
- used to automate tasks in Linux / UNIX
- shell script = set of commands executed by shell (CLI interpreter)

Creating a shell script:
- create file with `.sh` extension
- start with shebang → `#!/bin/bash`
- shebang tells which interpreter should run the script

Running a script:
- give execute permission → `chmod +x file.sh`
- run using `./file.sh`
- running with `sh file.sh` may fail for bash-specific features

Variables:
- declared as `VAR=value` (no spaces)
- convention → uppercase variable names
- access using `$VAR` or `${VAR}`
- user input using `read -p "prompt" VAR`

Conditionals:
- `if` used for decision making
- syntax uses `[ condition ]`
- `-f file` → check if file exists
- `[[ ... ]]` is bash specific

Loops:
- `for` and `while` used for iteration
- commonly used for files, users, repetitive tasks

File & directory management:
- `mkdir` → create directory
- `cd` → move between directories
- `touch` / `cat > file` → create files

Permissions:
- permissions apply to user, group, others
- `rwx` → read, write, execute
- modified using `chmod`
- `rm -rf` deletes recursively and forcefully (dangerous)

ACLs (Access Control Lists):
- provide fine-grained permissions
- allow multiple users / groups on same file
- viewed using `getfacl`
- set using `setfacl`
- default ACLs apply to newly created files inside a directory

String operations:
- uppercase → `tr [a-z] [A-Z]` or `${var^^}`
- lowercase → `${var,,}`
- reverse string using `rev`
- substring using `${var:pos:len}`

Text utilities:
- `tr`, `sed`, `awk` for text processing
- `find <path> -name <pattern>` for searching files
- regex used internally by many commands

Functions:
- used to reuse code
- defined as:
