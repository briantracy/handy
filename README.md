handy
=====
#### never `history | grep ...` again!


```
handy [<handyfile> [<copy paste program> [<command number>]]]
```


`handy` is a command line utility that helps you keep track of a list of handy commands. 

### Intro


### Handyfile Syntax
Each line in your handyfile is one of four things.

1. A comment (line starts with `#`)
2. A heading (line starts with `-`)
3. A handy command (line starts with `$`)
4. Whitespace

Here is an example of a basic handyfile:

```
# my handyfile 

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
Git commands
------------
1. git diff -- . ':(exclude)*.xib' | subl

Carthage commands
-----------------
2. carthage bootstrap --platform Mac --cache-builds

Git commands
------------
3. git diff -- . ':(exclude)*.xib' | subl

```

### Automatic Command Copying


### Shell Aliasing
Shell aliasing is crucial to the ease of use of `handy`. Beacuse you must at least specify a handyfile on every invocation of `handy` using an alias makes things much easier. For example, using bash:

	$ alias handy='handy /Users/myname/.handyfile <copy paste program>'
	
Now, you can just use

	$ handy [<optional command number>]


### Copy Paste Programs
Passing in a clipboard management program allows you to directly copy one of your handy commands. The following are possibilities you can use. 

| OS            | Copy Paste Program           
| ------------- |-------------
| MacOS         | `pbcopy` (builtin) 
| Linux         | `xclip` `xsel` `clipit`      