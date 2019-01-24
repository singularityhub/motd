# Message of the Day

for Singularity containers

> What is a message of the day?

If you've ever logged into a linux cluster, or played a computer 
game like Half Life or World of Warcraft, you might be greeted with some
asciiart, or something along the lines of a "tip of the day." This is more
official called a "message of the day," (short is [motd](https://en.wikipedia.org/wiki/Motd_(Unix)) 
and there is a bit of [history behind it](https://ownyourbits.com/2017/04/05/customize-your-motd-login-message-in-debian-and-ubuntu/). In short, we print a message to the terminal 
for the user to see when he or she first logs into a shell.

> How can we use motd with containers?

In the context of a container, we might want to give the user a friendly message
if they shell inside. The simplest use case is to greet the user. A more useful
use case is to provide some help for how to interact with the container, or
where to find documentation.

> How do we add motd to Singularity containers?

If we are creating a Singularity container,
we can't just echo a message in the runscript, because this gets executed on
a shell *or* a run. We need to edit the `/.singularity.d/actions/shell`
script that is executed **only** on a shell.

## Singularity MOTDs

In this repository, we will provide you with a few fun examples for generating
messages of the day in Singularity containers.

 - [greeting](greeting): a simple message of the day to greet the user
 - [help](help): show the container's %help section to the user when they shell inside
 - [asciiart](asciiart): generate a greeting with awesome asciiart!

Clearly, many of these examples are for fun, and others are better for communicating
information. I'm of the firm belief that we should aspire for both - interaction
with containers should be both informative and fun.
