# Makefile

## cannot use process substitution in makefile

### problem

Adding this as is into a Makefile fails:

```
all:
    diff <(echo test) <(echo test)
```

The error (hint: /bin/sh points to /bin/bash on this system):

```
/bin/sh: -c: line 0: syntax error near unexpected token `('
/bin/sh: -c: line 0: `diff <(echo test) <(echo test)'
```

### solution

When invoked as sh, bash will be running in POSIX mode (as if POSIXLY_CORRECT was defined, or it was started with --posix).
In this mode, process substitutions do not exist.

Define the Makefile variable SHELL as /bin/bash

```makefile
SHELL := /bin/bash
```

### ref

[bash - Process substitution in GNU Makefiles](https://unix.stackexchange.com/questions/356535/process-substitution-in-gnu-makefiles)

[Makefile上でprocess置換を使う方法](https://pod.hatenablog.com/entry/2020/04/02/063638)
