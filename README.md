# aliaser

A Shell CLI tool to conveniently manage aliases for bash and zsh.

## Installation
Clone the repository to your folder of choice:

    $ git clone https://github.com/bhayatus/aliaser.git .

Create a file that will contain your aliases if you aren't using one already:

    $ touch ~/.aliases

If you choose a different name for your aliases file, modify the following in the aliaser script:

    # Change ~/.aliases to your own file name
    alias_file=$(realpath ~/.aliases)

Add the following to one of .bashrc, .zshrc, or another startup script:

    alias aliaser="source <path to aliaser script>"
    # Change aliases file name here if necessary
    source ~/.aliases

Ensure that you source your newly modified startup script like so:

    $ source ~/.bashrc

## Usage
Running `aliaser help` displays the following:
    
    CLI tool to manage aliases for bash and zsh

    usage: aliaser <operation> [alias] [command]

    operations:
        ls
                Lists all aliases saved in the aliases file

        add <alias> <command>
                Creates/replaces an alias for the specified command in the aliases file
                The alias name must not contain any spaces
                If command contains spaces, it must be wrapped in quotes

        rm <alias>
                Removes the alias permanently from the aliases file
                The alias name must not contain any spaces

        help
                Prints the help text

    Visit https://github.com/bhayatus/aliaser for details on setup

Note that this tool only manages aliases stored within the aliases file, any declared outside will not be affected.

## Examples

    $ helloworld
    helloworld: command not found
    $ aliaser ls
    No aliases found in /home/bhayatus/.aliases
    $ aliaser add helloworld "echo \"hello world\""
    Added alias 'helloworld'
    $ helloworld
    hello world
    $ aliaser ls
    alias helloworld='echo "hello world"'
    $ aliaser rm helloworld
    Removed alias 'helloworld'
    $ helloworld
    helloworld: command not found

    $ ll
    ll: command not found
    $ aliaser add ll "ls"
    Added alias 'll'
    $ ll
    projects  test.txt
    $ aliaser add ll "ls -la"
    Alias 'll' already exists, replace? (y to continue) y
    Added alias 'll'
    $ ll
    total 16
    drwxr-xr-x 3 bhayatus bhayatus 4096 Dec 14 18:18 .
    drwxr-xr-x 9 bhayatus bhayatus 4096 Dec 14 23:50 ..
    drwxr-xr-x 3 bhayatus bhayatus 4096 Dec 14 11:43 projects
    -rw-r--r-- 1 bhayatus bhayatus   92 Dec 14 18:20 test.txt
