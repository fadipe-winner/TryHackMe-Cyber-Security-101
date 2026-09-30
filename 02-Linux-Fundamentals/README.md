# Linux Fundamentals (Parts 1–3) | TryHackMe Cyber Security 101

My notes and hands-on practice from the Linux Fundamentals rooms in TryHackMe's Cyber Security 101 path. I connected to the lab machine over SSH and worked through everything from the terminal.

## What I Learned

- **Navigating and managing files:** creating, copying, moving and deleting files and folders from the command line.
- **Getting help:** using `--help` and `man` pages to see what a command can do instead of guessing.
- **Key directories:** knowing where things live on a Linux system matters when you need to find evidence.
- **Users and editors:** switching users, reading files, and editing with `nano` and `vim`.
- **Transferring files:** downloading with `wget`, copying between machines with `scp`.
- **Processes and services:** viewing, stopping and managing what is running.
- **Automation and maintenance:** cron jobs, installing software with `apt`, and where logs are stored.

## What I Practised

- Connected to the lab machine using SSH.
- Used `ls --help` and `man` to explore command options.
- Created, copied, moved and removed files and directories.
- Switched between users and read file contents.
- Edited files with `nano`.
- Listed running processes with `ps aux` and `top`.
- Used `kill` and `systemctl` to manage processes and services.
- Ran a command in the background and brought it back to the foreground.

## Commands I Used

| Area | Commands |
|---|---|
| Remote access | `ssh user@<lab-ip>` |
| Help | `ls --help`, `man <command>` |
| Files | `touch`, `mkdir`, `cp`, `mv`, `rm`, `cat` |
| Users | `su - <user>` |
| Editors | `nano <file>`, `vim <file>` |
| Transfers | `wget <url>`, `scp`, `curl` |
| Processes | `ps aux`, `top`, `kill <PID>` |
| Services | `systemctl start / stop / enable / disable / status <service>` |
| Jobs | `command &` (background), `fg` (foreground) |
| Scheduling | `crontab -e` |
| Packages | `apt`, `add-apt-repository` |
| Logs | `/var/log` |

## Directories Worth Remembering

| Directory | What It Holds |
|---|---|
| `/etc` | System configuration files |
| `/var` | Variable data that services write often, including logs in `/var/log` |
| `/root` | Home folder of the root user |
| `/tmp` | Temporary files, cleared on reboot |

## Process Signals

| Signal | What It Does |
|---|---|
| `SIGTERM` | Asks the process to terminate cleanly |
| `SIGKILL` | Stops it immediately |
| `SIGSTOP` | Pauses it |

## Cron Format

```
MIN  HOUR  DOM  MON  DOW  CMD
```

Each line in a crontab is one scheduled job: which minute, hour, day of month, month and day of week to run, followed by the command.

## Challenges and Mistakes

**Copying a file to a remote system with `scp`.** I tried to copy a file from my current system to a remote system and got stuck for about two hours, not understanding what I was doing wrong.

The problem was that I was running `scp` from the wrong machine. I was still logged into the remote system over SSH, so my terminal was working on the remote machine instead of my own. `scp` has to be run from the machine that is doing the copying. Once I understood that, I left the SSH session and ran it from my own system.

```bash
# Run from MY machine, not from inside the SSH session
scp <file> user@<remote-ip>:<remote-path>
```

**Lesson:** when a command behaves strangely, I first check which machine I'm actually on. The terminal prompt shows it, and so does `hostname`. A lot of confusing problems come down to running the right command in the wrong place. This also matters in SOC work, where acting on the wrong host during an investigation can be a real mistake.

## Why This Matters for SOC / Blue Team Work

- **Logs:** most Linux investigations start in `/var/log`. Knowing where logs live is the first step of any investigation.
- **Processes:** spotting an unfamiliar process with `ps aux` or `top` is a basic way to find suspicious activity on a host.
- **Cron:** attackers often use scheduled jobs to keep access to a machine. Knowing how cron works helps me know what to check.
- **Users and permissions:** understanding who can do what helps me judge whether an action was normal or suspicious.
- **Services:** checking what starts at boot is part of reviewing a compromised system.
- **Transfers:** `wget`, `curl` and `scp` are also how files move in and out of a machine, which matters when reviewing suspicious activity.

## Key Takeaway

The Linux command line is less about memorising commands and more about knowing where to look and where you are. My two-hour `scp` problem taught me to check which machine I'm on before anything else, and I now see why logs, processes and scheduled jobs are the first places a SOC analyst looks.

## Next Step

A small investigation using what I learned here: SSH into a lab machine, list running processes, check `/var/log` for login activity, and review cron jobs, then write up what I found.
