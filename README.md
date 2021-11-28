# JBuild
*A simple project generator for C/C++/CUDA.*

## Dependencies
JBuild has one mandatory and two optional dependencies:
 - zsh (mandatory: it's written in zshell)
 - git
 - curl
However, these are recommended (git will be used to initialize your project as a repository and curl is used to quickly pull licenses from GitHub).

For building projects made by JBuild, you'll need GCC (which come with gcc and g++) and possibly nvcc (for CUDA projects).

## Arguments and options
Let me just show you the help, that should clarify everything:
```
+------------------------------------------+
|                  JBUILD                  |
+------------------------------------------+
  A simple project generator for C/C++/CUDA

Creates a new project (with structure) in a subdirectory

 SYNOPSIS:
 ---------
 jbuild name [-c compiler] [-o optimization level] [-s strictness]
     [-i] [-u] [-d debug flag] [-t project type] [-e extra compile flags]
     [-l linker args] [-n license] [--no-git] [--no-init-commit]
     [--no-readme]

 only the name parameter is mandatory, all others have a default value

 PARAMETERS:
 -----------
 -c --compiler: (default: gcc)
     Sets the compiler. This should be one of `gcc`, `g++`, or `nvcc`.
     This compiler will be used for all of preprocessing, compilation
     and linking.

 -o --opti: (default: 0)
     Sets the optimization level. Valid values are `0`, `1`, `2`, `3`,
     `fast`, `g` and `s`. See the gcc help for more info.

 -s --strictness: (default: warn)
     Sets the strictness (impacts the number of warnings/errors). Valid
     values are (in order least to most strict): `off`, `warn`, `extra`,
     `pedantic`. Adding `+e` to any of the options (e.g.: `warn+e`) turns
     all warnings into errors.

 -i --install:
     Generates an install target as well (`make install`). Behaviour
     depends on the output type:
       - For executables: copies the executable to `/usr/bin`
       - For libraries (static & shared): copies the library to
           `/usr/lib/`, and the headers to `/usr/include`.
     This flag is off by default.

 -u --uninstall:
     Generates an uninstall target as well (`make uninstall`). This also
     enables the --install flag. This target removes the files created by
     the install target.
     This flag is off by default.

 -d --debug:
     Creates an extra target (`make debug`), which is compiled with `-D[value]`
     and `-g -O0` in addition to the other flags. The value passed has to be
     a valid C/C++ macro name.
     Debug targets are disabled by default.

 -t --output-type: (default: exec)
     Specifies the output type (also impacts the behaviour of -i and -u).
     Valid options are `exec` (executable in bin/[name]), `lib` (static
     library in lib/lib[name].a) and so (shared library in lib/lib[name].so).

 -e --extra-flags:
     Passes the given extra flags/arguments to the compiler for compilation.
     Contrarily to most other options, this one is stacked (all occurences
     append values).
     By default, no extra flags are passed.

 -l --link-args:
     Passes the given extra flags/arguments to the compiler for linking.
     Contrarily to most other options, this one is stacked (all occurences
     append values). Specify all needed libraries to link here (with -l).
     By default, no extra flags are passed.

 -n --license:
     Downloads the given license from GitHub and adds it to your project.
     Valid values to pass can be obtained by running the following command:
        `curl https://api.github.com/licenses | grep key`
     or by running `jbuild help license`.
     By default, no license is added.

 --no-git:
     Disables the creation of a git repository.
     By default, a new repository is created in the newly created project
     directory (along with a simple, default gitignore).

 --no-init-commit:
     Disables the (default) first commit with the following message:
        `Initial commit (using jbuild)`
     By default, the commit is created.

 --no-readme:
     Disable generation of the default one-liner README.md.
     By default, a README.md is generated with as contents:
        `# [project name]`

 RESULTING PROJECT STRUCTURE:
 ----------------------------
 For projects generated with `-t exec`
     .
     └── [name]/
         ├── bin/
         ├── inc/
         ├── LICENSE
         ├── Makefile
         ├── obj/
         ├── README.md
         └── src/

 For projects generated with `-t lib` or `-t so`
     .
     └── [name]/
         ├── inc/
         ├── lib/
         ├── LICENSE
         ├── Makefile
         ├── obj/
         ├── README.md
         └── src/
```
