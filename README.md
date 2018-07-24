handy
=====
#### never `history | grep ...` again!


```
handy [<handyfile> [<copy paste program> [<command number>]]]
```

### Intro
`handy` is a simple utility that allows you to bring up a list of useful commands that you can't seem to remember or don't want to type. Executing `handy` prints an ordered list of your commands. When you see the one you were looking for, give it's number to `handy` and the program will automatically copy it into your clipboard. 

### Handyfile Syntax
Each line in your handyfile is one of four things.

1. A heading (line starts with `-`)
2. A handy command (line starts with `$`)
3. A directive (line starts with `*`)
4. A comment (anything not above)

Here is an example of a basic handyfile:

```
This is my handyfile 
All lines are comments unless specifically denoted

- Git Commands
$ git diff -- . ':(exclude)*.xib' | subl

- Carthage commands 
$ carthage bootstrap --platform Mac --cache-builds

- Tar commands
$ tar cvxf <tarfile> <directory>
```
This will automatically be converted to the following when you invoke `handy`.

```
$ handy /path/to/handyfile
=== Git commands ===
1. git diff -- . ':(exclude)*.xib' | subl

=== Carthage commands ===
2. carthage bootstrap --platform Mac --cache-builds

=== Git commands ===
3. git diff -- . ':(exclude)*.xib' | subl

```

Lets say that I wanted to do a `carthage bootstrap` (command 2). All I have to do is pass my copy paste program and command number to handy, and it will do the rest. 

```
$ handy /path/to/handyfile pbcopy 2
$ # 'carthage bootstrap --platform Mac --cache-builds' now in buffer
```

### Automatic Command Copying


### Shell Aliasing
Shell aliasing is crucial to the ease of use of `handy`. Beacuse you must at least specify a handyfile on every invocation of `handy` using an alias makes things much easier. In addition, you might as well include the path to your copy paste program so you can invoke handy with 1 or 0 arguments. For example, using bash on macOS:

	$ alias handy='handy /Users/myname/.handyfile pbcopy'	
Now, you can just use

	$ handy [<optional command number>]


### Copy Paste Programs
Passing in a clipboard management program allows you to directly copy one of your handy commands. The following are possibilities you can use. You can use any clipboard manager that accepts input over `stdin`. 

| OS            | Copy Paste Program           
| ------------- |-------------
| MacOS         | `pbcopy` (builtin) 
| Linux         | `xclip` `xsel` `clipit`
| Windows       | `clip.exe` (builtin)   

### Directives
Along with comments, commands, and headings, the final type of line you can have in your `handyfile` is a directive. Directives tell `handy` to perform some specific action when executed. Currently, the only directive that is supported is `* wait-for-input`, which tells `handy` when invoked to print out your list of handy commands, then pause and listen to `stdin` for the number of the command you want to copy. This came about due to the common use case of calling `handy` with no arguments, finding the correct command, then having to re-call `handy` with a number. This can be done in one step. 

```
# Old
$ handy
=== Some Heading ===
1. ls -l 
$ handy 1

# New
$ handy # * wait-for-input is in handyfile
=== Some Heading ===
1. ls -l
enter command number: 1
$ # 'ls -l' now in clipboard

```

### FAQ
**Q** How do I install it. 
**A** 

```
$ curl -o /usr/local/bin/handy 'https://raw.githubusercontent.com/briantracy/handy/master/handy'
$ chmod +x /usr/local/bin/handy'
```

**Q** Is this free software? 
**A** Yes. 

**Q** What are the system requirements?
**A** Python 2

**Q** Does it ever require elevated priveledges?
**A** No. 

**Q** Does it leave a footprint on my computer?
**A** No. `handy` does not generate any files. 

**Q** How do I uninstall it?
**A** `rm /usr/local/bin/handy && rm ~/path/to/my/handyfile` (The second path is of course up to you)

**Q** 
**A**
