# tmux_quick_start

---

## Introduction
- I use a remote system for my work, which I connect through `ssh`. This remote system has no workload manager (such as Slurm), since it's only used by my lab, and it's not a cluster.
- I run processes (such as [STAR](https://github.com/alexdobin/STAR)), that can take days to complete. I use a MacBook to start a process that I connected to over ssh. If I turn off/close the MacBook (or even worse, if the MacBook goes to sleep to conserve battery!), the job is killed. That's very annoying.
	- In the past, I used `nohup` (check with `man nohup`) to prevent my jobs from being killed when my terminal session ends. It gets the job done, it's fine. But `tmux` does this and so much more.

## tmux
- What is tmux?
	- I like to think of it as 'virtual screens' that are floating in space. You can 'grab' any screen at anytime, `attach` it to your terminal session and use it as your 'active window'.
	- If you want to stop working on it for the time being, or switch to another free floating virtual screen, you can `detach` your session, and `attach` another session that you create/already been created in the past.
- Why use tmux?
	- keep a session running all the time (think of it as different workspaces that can be left open in the background for you to access whenever you want!)
	- Work with multiple projects simultaneously, and independently, and quickly exit and enter these setups as needed (similar to arranging specific tabs within an IDE based on your project needs)
	- If you're working from a remote computer that's not used by many others, and the remote has no workload manager, tmux is a great solution.
	- Run multiple independent processes in a remote server simultaneously and monitor their progress regardless of whether you're actively connected or not

# Get started with basic tmux

#### tmux prefix key
- most tmux commands don't work as 'linux' commands, but instead as a bunch of keybindings. All of these keybindings start with a prefix (by default it's `ctrl+b`)
	- I personally changed the keybindings to `ctrl+q`, since it's easier to reach when the keybindings are used often (especially when you remap your mac caps lock key with ctrl, but that's another story).
- The commands with the key binds work only when you're in a tmux session (duh)

Here's some tmux commands you'll use often :

1. create a new session called "oregon" : `tmux new -s oregon`
2. Detach current session : `prefix+d` (Note : This also kills any of the processes being run)
3. split pane right : `prefix+[`
4. split pane bottom : `prefix+]`
5. close current pane (if there's multiple panes) - `prefix+x`

## The tmux.config file (located in `~/.tmux.conf`)
- Just like other Unix tools such as `vim`, there's a tmux config file which can be used to customize `tmux` as much as you like.
- One important tmux.conf entry is enabling mouse actions (called the "mouse mode", which allows you to click between different tmux panes instead of using the keybindings every time you want to switch to a different pane (which is a huge win)
- Most of the customizations I've done are changes to the keybindings, and more visually appealing bars at the bottom to display the current tmux session status (such as the name, and even the weather!). My tmux.conf file is attached in this repository if you're interested in taking a look.
- You can also use third party tmux plugins (some of which are included in my tmux config file). Check the link at the end if you want to look more into the third party tmux plugins. 

## Typical tmux use case examples:
Here are some examples of where you can use tmux to get your job done
- Run a command that can take hours to run, and close the session and resume your other activities (tmux will be running in the background, hence the process is always running). Reattach the session anytime to monitor the progress and check if the process has stopped due to errors of some kind.
- If you're working on a multicode project : If I'm not wrong, emacs (vim, to a lesser extent) has a ton of extensions and settings to be used as a full-blown IDE, but here's how I mix tmux and vim to develop longer codes in a remote session: 
<img width="1440" alt="image" src="https://github.com/artorias111/tmux_quick_start/assets/48955393/add294f9-210d-48d4-817a-d3db821d01d4">


- I view my code in the long left pane, view any data needed on the top right, and run the python script in the bottom left. I can `detach` this setup, return to my normal terminal and re`attach` this whenever I want (even if the code in vim is unsaved, it's maintained in the same state that you `detach` it in).
	- Note that this is how I do it, there's certainly more creative ways to use code editors with tmux, whatever works for you!
- The best part of this setup is that if you want to quit and come back to it later, it's as easy as detaching and reattaching the same session anytime later, and it's going to exist in the same state when you reattach (even if you haven't saved the changes in your editor!)


For more information, look at https://medium.com/hackernoon/a-gentle-introduction-to-tmux-8d784c404340

For customizing your tmux config file, take a look at https://www.hostinger.com/tutorials/tmux-config 
