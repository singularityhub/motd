# Greeting

Here is how you can add a simple greeting to your Singularity containers!
The recipe also demonstrates using an environment variable to reference
the user by name:

## Singularity 3.0+

```bash
%post
    # Write an echo statement to the second and third line of the shell action
    cat > /.singularity.d/env/99-motd.sh <<EOF
case \$0 in
    /.singularity.d/actions/shell)
        echo "Hello \$USER!"
        echo ;;
esac
EOF
```

## Singularity Under 3.0

**One Line Greeting**

```bash

Bootstrap: docker
From: ubuntu:16.04

%post

    # Write an echo statement to the second line of the shell action
    sed -i '2iecho Hello, ${USER}!' /.singularity.d/actions/shell

```

The reason we want to add to the **second** line and not the first is because
the first line is theinterpreter line (`#!/bin/sh`). But guess what? You can add
another echo (or just a new line) by doing the following:

**Multiple Lines**

```bash
%post

    sed -i '2iecho Hello, ${USER}!;' /.singularity.d/actions/shell
    sed -i '3iecho;' /.singularity.d/actions/shell
```

## Build

You can build the container as follows:

```bash
$ sudo singularity build greeting.sif Singularity
```

And then try running a shell to see the greeting.

```bash
$ singularity shell greeting.sif

$ singularity shell greeting.sif
Singularity: Invoking an interactive shell within container...

Hello, vanessa!

Singularity greeting.sif:~/Documents/Dropbox/Code/singularity/motd/greeting>
```

It doesn't technically matter how you choose to edit the file during %post -
just make sure that you write to the `/.singularity.d/actions/shell` file,
and don't muck up any of the goodness already in there.
