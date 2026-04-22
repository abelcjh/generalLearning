# local vs wsl
local extensions run in windows
handle ui, themes, keyboard shortcuts, and actual connection to wsl

wsl extensions run in linux
access linux files and compilers

# access windows applications

## error
when just type 'cursor' in wsl, invoking cursor.exe windows application
but windows process cannot see linux environment variable in .bashrc
chromium engine in cursor.exe boot up,
cant find windows crash reporting pipeline in wsl,
just dump debug log file into repo

### need wslenv bridge
tell linux, pass environment variable through firewall into windows when run command
use microsoft's undocumented wslenv flag

open ~/.bashrc file, add these lines:
```bash
# 1. set the variable in linux
export ELECTRON_DISABLE_LOGGING=1

# 2. force wsl to pass this variable to windows applications (/u flag)
export WSLENV="ELECTRON_DISABLE_LOGGING/u:$WSLENV"
```

/u flag tells wsl, when run windows application, inject variable into windows
save .bashrc file, run ~/.bashrc file