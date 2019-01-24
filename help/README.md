# Singularity Help MOTD

A few years ago I added the [%help](https://github.com/sylabs/singularity/pull/843) section to the singularity recipe. The idea was that if you wrote this section in your [Singularity](Singularity)
recipe, the user could ask your container for help!

```bash
$ singularity help helpme.sif


Oh, hi there! This is the help section. Here is how to run the container:
    singularity run <container>

Here is how to shell into the container:
    singularity shell <container>

Here is how to execute a custom command
    singularity exec <container> ls /


```

But there is one problem here, we are still relying on the user to type that
command in the first place! This is a great use case for message of the day
(motd) - we can show this same help script when the user shells into the container!
Here is what the Singularity recipe looks like:


```bash
$ singularity shell helpme.sif 
Singularity: Invoking an interactive shell within container...



Oh, hi there! This is the help section. Here is how to run the container:
    singularity run <container>

Here is how to shell into the container:
    singularity shell <container>

Here is how to execute a custom command
    singularity exec <container> ls /


Singularity helpme.sif:~/Documents/Dropbox/Code/singularity/motd/help> 
```

It would be more informative to have paths or other usage that a user shelling
into the container might need. Or you could add dependencies for usage like mounting a particular
directory, or setting an environment variable.
