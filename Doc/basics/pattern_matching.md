
# Pattern Matching

## Classic pattern matching

Classic pattern matching, support of glob (\*), single character (?), ranges ([a-z]) and brace ({}) expansions, pattern lists (?(), \*(), +(), @(), !()).

The '%' specifier must be used :

```bash
echo "t?t?" # prints 't?t?'
echo %"t?t?" # prints whatever filenames match 't?t?'
```

Note : in interactive mode, pattern matching is used on double-quote strings without the need for the '%' modifier.

```bash
pat='t?t?'
ls %pat
echo %'pl?p'
```

The `%` is the expand operator.

## Regex pattern matching

Support for posix regex, works only with the %E specifier :

```bash
echo %E'/(t[aeiou]){2}/' # will match tata, tete, titi, toto, tutu file names
```

## Using pattern matching on any text content

Pattern matching can be used on any content (not only file system) with the < modifier :

```bash
echo %'pl[aeiouy]p'<(cat /etc/passwd) # in that case the input feed used for pattern-matching is a command's output. Buffers and named pipes can be used as well
```

Notes :

- when used with streams (inputs, buffers ...) pattern matching will consider lines. To use pattern matching with other separators, the separator must be speciefied befor the '%' modifier :
- the redirect operator must be sticked to the string (`'<`).

```bash
echo %E'/^[A-Z]+$/'<buffer

# works with list of separators :
seps=[]
seps[]=" "
seps[]="\t"
seps[]="\r\n"
seps[]="\n"
echo seps%E'/^[A-Z]+$/'<:namedpipe
```

