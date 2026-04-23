# .bashrc
stands for bash run commands
a config script
the startup routine for terminal, every time open wsl terminal will run bashrc file before type first command

this does not auto update specific config files of apps

but if put in bash rc file, all programs can see and use

## how to put configs in bash rc file
open file in cursor
add the line export ... = ""
back in terminal, run source ~/.bashrc

/u flag tells wsl, when run windows application, inject variable into windows