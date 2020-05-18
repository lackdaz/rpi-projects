# Basics

## Cron
To start, type

  `crontab -e`

  to access your user's crontab file, or

  `sudo crontab -e`

  to access the root crontab

Each entry is represented by five time-and=date fields followed by a command and a newline char.

__Example__

| minute (0-59) | hour (0-23) | day (1-31) | month (1-12) | weekday (0-6, 0=Sunday)| Remarks |
|:---:|:---:|:---:|:---:|:---:|:---:|:--|
| 00 | 07 | * | * | * | Will trigger at 7am everyday |
