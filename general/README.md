# General

Here is a general recipe to customize interaction with the user during run,
shell, test, or exec.

```
%post
    cat > /.singularity.d/env/99-motd.sh <<EOF
case \$0 in
    /.singularity.d/actions/shell)
        echo "Hello \$USER from shell" ;;
    /.singularity.d/actions/exec)
        echo "Hello \$USER from exec" ;;
    /.singularity.d/actions/run)
        echo "Hello \$USER from run" ;;
    /.singularity.d/actions/test)
        echo "Hello \$USER from test" ;;
esac
EOF
```

## Build

You can build the container as follows:

```bash
$ sudo singularity build greeting.sif Singularity
```

And then try running a shell, exec, run, or test to see the greetings.

```bash
$ singularity shell greeting.sif 
Hello vanessa from shell
Singularity greeting.sif:~/Documents/Dropbox/Code/singularity/motd/general> exit
```
```bash
$ singularity exec greeting.sif echo "Another hello"
Hello vanessa from exec
Another hello
```
```bash
$ singularity run greeting.sif
Hello vanessa from run
$ exit
```
```bash
$ singularity test greeting.sif
Hello vanessa from test
No Singularity container test found, executing /bin/sh -c true
```
