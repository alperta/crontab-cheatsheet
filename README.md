# Crontab Cheatsheet

Crontab (cron table) is a Unix-based job scheduling program that allows users to schedule jobs (commands or scripts) to run periodically at fixed times, dates, or intervals.


## Format of a Cron Job

A cron job is defined by a line in the crontab, with the format:

```
* * * * * command-to-be-executed
- - - - -
| | | | | 
| | | | +---- Day of the week (0 - 7) [Both 0 and 7 represent Sunday]
| | | +------ Month (1 - 12)
| | +-------- Day of the month (1 - 31)
| +---------- Hour (0 - 23)
+------------ Minute (0 - 59)
```

## Common Operators

- `*`: represents every possible value for the field.
- `-`: represents a range of values.
- `,`: specifies a list of values.
- `/`: specifies increments.

## Examples

1. Run `my-command` at 5:30 every morning:
```
30 5 * * * my-command
```

2. Run `my-command` every 15 minutes:
```
*/15 * * * * my-command
```

3. Run `my-command` at 2:30pm on the first day of every month:
```
30 14 1 * * my-command
```

4. Run `my-command` at 10 pm from Monday to Friday:
```
0 22 * * 1-5 my-command
```

5. Run `my-command` every month in January, March, and May at 3:15pm:
```
15 15 * 1,3,5 * my-command
```

## Crontab Commands

- `crontab -e`: Edit your crontab.
- `crontab -l`: List your crontab.
- `crontab -r`: Remove your crontab.
- `crontab -u <username> -e`: Edit crontab for another user (requires appropriate permissions).

## Special Strings

These strings represent special schedules:

- `@reboot`: Run once at startup.
- `@yearly` or `@annually`: Run once a year, i.e., "0 0 1 1 *".
- `@monthly`: Run once a month, i.e., "0 0 1 * *".
- `@weekly`: Run once a week, i.e., "0 0 * * 0".
- `@daily` or `@midnight`: Run once a day, i.e., "0 0 * * *".
- `@hourly`: Run once an hour, i.e., "0 * * * *".

For example, to run `my-command` at startup:
```
@reboot my-command
```

## Tips

- Ensure that any scripts or commands being called by your cron jobs have absolute paths to avoid confusion.
- If you're storing output or logs, it's also wise to use absolute paths.
- It can be helpful to redirect the output of your cron jobs to a log for debugging purposes. E.g., `30 5 * * * my-command >> /path/to/logfile 2>&1`.
