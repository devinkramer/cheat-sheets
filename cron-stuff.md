# Cron Syntax

  *     *    *    *    *  command to be executed
  -     -    -    -    -
  |     |     |     |     |
  |     |     |     |     +----- day of week (0 - 6) (Sunday=0)
  |     |     |     +------- month (1 - 12)
  |     |     +--------- day of month (1 - 31)
  |     +----------- hour (0 - 23)
  +------------- min (0 - 59)

## Dont be a dork add this to your cron jobs so you box is not sending your lame SDTOUT and STDERR to an non-existing email box.
```bash
>/dev/null 2>&1
```
# Examples
## Example log file find and compress cron
```bash
0 22 * * * find /data/singles/tomcat/logs/photos??_access_log.????-??-??.txt -mtime +10 -print -exec nice /bin/gzip {} \; > /dev/null 2>&1 
```
## Example cron for finding and removing log files
```bash
30 23 * * * find /data/singles/tomcat/logs/server.log.????-??-??.gz -mtime +30 -print -exec rm -f {} \; > /dev/null 2>&1 
```
