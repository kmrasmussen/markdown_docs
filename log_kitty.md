# How I Log Everything From All Kitty Terminal Windows

Using a script `auto_script2.sh` which is 

```
Bash script for generating screen log files with date, time, and random number

#!/bin/bash

# Generate the current date and time
DATETIME=$(date "+%Y%m%d_%H%M")

# Generate a large random number
RANDOM_NUM=$(shuf -i 100000-999999999 -n 1)

# Construct the log file name
LOG_FILE="screen_${DATETIME}_${RANDOM_NUM}.log"

# Execute the script command
exec script -f -c "exec fish" "$HOME/scriptheap/mshell/slogs/$LOG_FILE"
```

and do
```
chmod +x auto_script2.sh
```

and in kitty config `~/.config/kitty/kitty.conf`
I have the line `shell /home/kasper/scriptheap/mshell/auto_script2.sh`