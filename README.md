# aliaser

A `Shell` CLI tool to conveniently manage aliases for `bash` and `zsh`.

## Installation

If you are using a `Debian` flavor of `Linux` such as `Ubuntu`, download the latest `.deb` file from the `Releases` section, and run the following:

    $ sudo dpkg -i aliaser_*.deb

Alternatively, you can do the following:

    $ git clone https://github.com/bhayatus/aliaser.git
    # Move the script to a location within your PATH.
    $ sudo cp aliaser/aliaser /usr/local/bin

Next, create a file that will contain your aliases (if you aren't using one already):

    $ touch ~/.aliases

Add the following to a startup script such as `.bashrc` (or `.zshrc` if you are on `macOS`):

    export ALIASES_FILE=~/.aliases
    source $ALIASES_FILE

    # Necessary if you don't want to restart your current session for changes to take effect.
    aliaser () {
      command aliaser "$@"
      if [ $? -eq 0 ]; then
        if [ $1 = "add" ]; then
          source $ALIASES_FILE
        elif [ $1 = "rm" ]; then
          unalias $2 &> /dev/null
        fi
      fi
    }

Ensure that you source the updated `.bashrc` (or `.zshrc` if you went that route):

    $ source ~/.bashrc

## Usage

Running `aliaser help` displays the following:

    Tool for managing bash/zsh aliases

    usage: aliaser <operation>

    operations:
        ls
              Lists all aliases saved in the aliases file, in alphabetical order

        add <alias_name> <command>
              Creates/replaces an alias for the specified command in the aliases file

              The alias name must not contain any spaces, and can only consist of alphanumeric characters

              In the event that you need to add an alias for a more complex command or an alias that contains several,
              you can wrap with double quotes, i.e. $ aliaser add print_temp "cd temp && ls"

              If you need to escape a character in the command, use a preceding \

        rm <alias_name>
              Removes the alias permanently from the aliases file

              The alias name must not contain any spaces

        help
              Shows the help display

        version
              Shows the current version

    Visit https://github.com/bhayatus/aliaser for details on setup

Note that this tool only manages aliases stored within the aliases file, any declared outside will not be affected.

## Demo

![Demo](demo.gif)
