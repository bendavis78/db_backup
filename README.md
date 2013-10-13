db_backup
=========

This script, intended to be run as a cron job, will create and maintain
rotated database backups on a daily, weekly, and monthly basis. By default,
this script will keep 7 daily backups, 5 weekly backups, 12 monthly backups,
and unlimited yearly backups. Weekly backups are made on Sunday (weekday "0"),
monthly backups are made on the first of the month ("01"), and yearly backups
are made on Jan 1 "01/01". These defaults can be overridden in a configuration
file placed in /etc/db_backup.conf. You may also override these for a specific
database in /etc/db_backup.conf.d/db_name. See "Default Settings" below for
details. 

Set up a cron job for each database you want to back up, calling this script
and passing the database name. For example:

    # m h dom mon dow user     command
      0 3 *   *   *   postgres /path/to/db_backup.sh example_database
      0 4 *   *   *   postgres /path/to/db_backup.sh another_database

This will run backups for "example_database" at 3am and "another_database" at
4am. If you want specific pg_dump arguments passed when creating the backup,
you may pass those arguments to this script after the database name. You may
also set pg_dump arguments in the DUMP_ARGS configuration setting.

Default Settings
----------------
These can be copied into either /etc/db_backup.conf for all databases, or into
/etc/db_backup.conf.d/db_name for a specific database.

    BASE_DIR="/var/db/backups"
    KEEP_DAILY=7
    KEEP_WEEKLY=5
    KEEP_MONTHLY=12
    WEEKLY_ROTATE_WEEKDAY="0"
    MONTHLY_ROTATE_DAY="01"
    YEARLY_ROTATE_DATE="01/01"
    DUMP_ARGS=""

