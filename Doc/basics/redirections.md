
# Redirections

## Simple Redirections

Open file/buffer for reading as standard input. file/buffer must exists.

```
cat < file
```

Open/Create file/buffer for writing as standard output, truncate the file before writing.

```
cat > <file | buffer>
```

Combination of `<` and `>`. file/buffer must exists.

```
cat <> file/buffer
```

Open/Create file/buffer for writing as standard output,
append to the file/buffer if already exists.

```
cat >> file/buffer
```

Standard input is read until reading word or end of file.
word is not sent.
Every line is stored in a buffer before it is sent to the command

```
cat << word
```

Same as <<< but lines are sent while read.

```
cat <<< word
```

The standard input/output is closed before the command is executed.
Doesnt work with functions as it is done in the forked process.

```
cat <& >&
```

## Redirection modifiers

Redirections can be affected by 3 modifiers : 1, 2 and &.
1 and 2 specifies the standard or error input.
& is the combinaison of 1 and 2.

```
cat &> file
```

These modifiers can be append to specify an output :

```
cat >2
```

Note that you must escape the & modifier when used as an output :

```
cat >\&
```
