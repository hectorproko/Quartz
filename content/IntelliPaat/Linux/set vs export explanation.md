# Explanation

In the context of Unix-like operating systems and shell scripting (such as in the bash shell), `set` and `export` are commands that deal with environment variables, but they have different purposes and scopes:

1. **set**:
    - The `set` command is used to set shell options and positional parameters.
    - It can also display all the environment variables and shell attributes.
    - Variables set with `set` are local to the current shell.
    - Syntax for viewing all variables and their values: `set`
    - Syntax for setting variables: `set variable_name=value` (This is not standard and might not work in all shells; in bash, direct assignment like `variable_name=value` would be more common.)
2. **export**:
    - The `export` command is used to mark variables for export to the environment of subsequent commands (i.e., child processes).
    - By exporting a variable, you make it an environment variable and it becomes accessible to subprocesses.
    - If a variable is not exported, it is only known to the current shell (local variable) and is not passed to subprocesses.
    - Syntax for exporting a variable: `export variable_name=value`
    - Just marking an already declared variable for export: `export variable_name`
    - You can see variables exported with `printenv`
To illustrate the difference:

If you open a terminal and type:

```bash
variable1="hello"
```

`$variable1` will have the value "hello" in the current shell, but if you run a subprocess (e.g., `bash`), it won't know about `$variable1`.

However, if you do:
```bash
export variable2="world"
```

Then, `$variable2` will be known to any subprocess you run from the current shell because you've exported it.

In a practical sense, when you want a variable to be available to other processes or scripts that you might call from your current script or session, you'd use `export`. If you just need a variable within your current script or session, a simple assignment would suffice.

# Example
#chat

![[Pasted image 20230728120839.png]]

Certainly! Here's an example to illustrate the difference between a local variable and an exported (environment) variable when a subprocess is invoked.

Let's say we're using the `bash` shell.

1. **Without `export` (local variable)**:
```bash
local_variable="I am local" bash -c 'echo $local_variable'
```
When you run the above, the output will be blank, because the new shell (subprocess) created by `bash -c` doesn't have access to the `local_variable`.

2. **With `export` (environment variable)**:
```bash
export env_variable="I am global" bash -c 'echo $env_variable'
```

This time, the output will be:
```bash
I am global
```

This is because by using `export`, we made `env_variable` an environment variable that's available to subprocesses, including the new shell created by `bash -c`.

To give a real-world scenario, consider scripts that call other scripts or utilities. If the child scripts or utilities need to know about certain variables, those variables need to be exported in the parent script or session. Otherwise, the child processes won't have any knowledge of them.