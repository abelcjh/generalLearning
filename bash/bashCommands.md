# -la
-l, long listing
-a, all entries, including hidden names (start with .)

# curl
client url
command to transfer data to or from a server

-fssl, 4 flags
-f, fail silently on server errors, dont output error html
-s, silent, mute progress meter and error messages
-S, show error, used with -s, if command does fail, will still tell you why
-L, location, if file moved, redirect, tell curl follow link to new location

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```
use curl to download data from, or upload data to, the internet
here we are downloading an installation script
URL is where installation script is hosted
.sh extension indicates shell script
stdout become stdin for bash
bash, is the shell that reads and executes command scripts for computer

# sudo bash
give script administrative privileges, modify system files