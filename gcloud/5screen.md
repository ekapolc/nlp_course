## Screen ##

Normally, if you lost your internet connection while running a jupyter kernel, your work will be lost, since the shell will terminate along with jupyter. To make things easier, we recommend using
screen to manage your shell.

Screen is a session manager that multiplexes a physical terminal between several processes, typically interactive shells.

To launch screen

```
screen -U -S <session name>
```

**Note launching screen under my username will cause an error. Either do `sudo screen` or launch screen then `sudo su` inside the screen.**

You will be brought into a new shell session. This session will remain until you tell it to terminate.

To detach from this session (think of it as having the session runs in the background instead of the foreground), press CTL-A and CTL-D (one after the other). You will be brought back to the original terminal that launches the screen session.

To re-attach to the old session, do

```
screen -r <session name>
```

If you forget the session name, `screen -r` will list all the current active sessions (or automatically connects if there is only one session available).

Finally, to terminate the screen session, do

```
quit
```
when you're in a screen session.

We highly recommend you to launch Jupyter notebooks in a screen session.

Note: there is another alternative to screen called `tmux`. It can be configured to be more useful than screen, but is harder to use.
