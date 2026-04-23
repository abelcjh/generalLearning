# local vs wsl extensions
local extensions run in windows
handle ui, themes, keyboard shortcuts, and actual connection to wsl

wsl extensions run in linux
access linux files and compilers

# wsl cursor file not found error
error message: [0417/215251.461:ERROR:third_party\crashpad\crashpad\util\win\registration_protocol_win.cc:108] CreateFile: The system cannot find the file specified. (0x2)


this involves inter process communication (ipc)

## ipc
two programs on same computer talk to each other without saving data to hard drive
**note**: not two different os, but programs

windows ipc uses named pipes
linux ipc uses unix domain sockets

## why cursor need ipc
when launch `cursor.exe`, launch two programs
1) ui in windows
2) server in wsl

these are two separate processes, need ipc

cuz when use cursor with wsl,
split brain in half
ui (client) run in windows
backend (server) run in wsl

### why backend in wsl
cuz cursor started from wsl terminal, or inside cursor activate wsl connection, so cursor know files in wsl
cursor install headless vs code server in wsl
handle terminal, file searches, language servers like python or c++

when run cursor in wsl terminal, actually running linux shell script of this vs code server

so have wsl program, and windows program

## the problem - windows crashpad cannot find windows environment variable for ipc windows named pipe
run your command
run shell script of vs code server in wsl
run wsl node js process
relay ipc message to windows and read/write file, this is successful
but also cuz cursor built on electron libraries, invoke crashpad watchers in both wsl and windows

---

### why need a watcher
when program dies, cant write error report, connect to internet, send to devs
so this is the reason for chromium crashpad library, crashpad is the watcher
watcher get crash data from memory send to devs

there is a crashpad in windows for ui, and crashpad in wsl for server

this is about telemetry (see more below)

---

so
by right windows environment variables passed to wsl
for vs code windows has dedicated ipc sockets to provide those windows environment variables
but for cursor there is environment stripping, terminal clean no variables
this happens inside cursor, in integrated terminal
so start cursor in integrated terminal
cursor ui in windows need windows environment variable to start crashpad in windows
but cant find it, so write error into `debug.log` file

### why ipc to read/write wsl files successful
first there's another ipc, between wsl terminal and cursor server in wsl, this good
then also need send wsl files to cursor ui in windows, this also ipc, but not thru pipes or sockets
this part look at network file sharing, section below

---

## failed fix - wslenv bridge doesnt work
tell linux, pass environment variable through firewall into windows when run command
use microsoft's undocumented wslenv flag
this doesnt fix bug, cuz environment stripping, no variable alr

---

## current temp fix 
open ~/.bash_aliases file, refer to current bash aliases file for what to do
basically change file path to absolute path, run the cursor command in a temp folder, dump error log there, delete whole folder

---

---

# telemetry
automated process of app collect data about itself, send back to mothership ie developers

## telemetry uses
### usage analytics
record which buttons clicked, how long commands run, extensions used

#### crashpad (crash reporting)
if background process dies, crashpad takes computer memory snapshot, send it to main app so devs can fix bug

# windows and wsl network file sharing
when just type 'cursor' in wsl, this refers to cursor executable file in windows
network file sharing created cuz windows still need to read linux files
two things - network, and file sharing
set up hidden network connection (hyper-v)
use specialized protocol called plan 9 file system protocol (9P)

## wsl in windows
runs inside lightweight hyper-v virtual machine

windows send network request over this virtual network to linux kernel
hidden 9p server in wsl, receive request, read file from wsl ext4 hard drive, stream text back over network to windows

under 9P (?), use Custom RPC (Remote Procedure Call) Network Bridge, this replaces ipc pipes and sockets,
it's a dedicated translated network socket pass json messages

# why ~ works in standalone wsl terminal not in cursor integrated terminal
in standalone, translate wsl path into windows path
in integrated, cursor server has shell script, just give the raw thing with ~ to windows, cant read

# windows environment variables
windows will pass down env variables into wsl INTEGRATED terminal in ide