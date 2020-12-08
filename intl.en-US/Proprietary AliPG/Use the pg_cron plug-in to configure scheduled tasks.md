# Use the pg\_cron plug-in to configure scheduled tasks

This topic describes how to use the pg\_cron plug-in of ApsaraDB RDS for PostgreSQL. This plug-in allows you to configure scheduled tasks.

The pg\_cron plug-in is based on CRON and used for job scheduling. It uses the same syntax as standard CRON expressions. However, it can initiate PostgreSQL commands from databases.

Each scheduled task consists of the following two parts:

-   Schedule

    The schedule based on which you want to run the pg\_cron plug-in. For example, the schedule specifies to run the pg\_cron plug-in once every minute.

    The schedule follows the same syntax as standard CRON expressions. In this syntax, a wildcard \(**\***\) specifies to **run the pg\_cron plug-in at any time**, and a specific number specifies to **run the pg\_cron plug-in only during the time period that is specified by this number**.

    ```
     ┌───────────── Minute: 0 to 59
     │ ┌────────────── Hour: 0 to 23
     │ │ ┌─────────────── Date: 1 to 31
     │ │ │ ┌──────────────── Month: 1 to 12
     │ │ │ │ ┌───────────────── Day of the week: 0 to 6 (The value 0 indicates Sunday.)
     │ │ │ │ │                  
     │ │ │ │ │
     │ │ │ │ │
     * * * * *
    ```

    The following schedule specifies to run the pg\_cron plug-in at Greenwich Mean Time \(GMT\) 3:30 in the morning on every Saturday:

    ```
    30 3 * * 6
    ```

-   Task

    The task that you want to execute. Example: `select * from some_table`.


## Precautions

-   Scheduled tasks run based on GMT.
-   Scheduled tasks are stored in a default database named postgres. However, you can query scheduled tasks in other databases.
-   The pg\_cron plug-in is upgraded. If you started using the plug-in before the 20201130 minor version, you must re-create the plug-in to obtain the new features. However, after the plug-in is re-created, the scheduled tasks that are created in the original plug-in are lost. For more information, see [Release notes of minor AliPG versions](/intl.en-US/Proprietary AliPG/Release notes of minor AliPG versions.md).

## Basic usage

-   Create the pg\_cron plug-in.

    ```
    CREATE EXTENSION pg_cron;
    ```

    **Note:** Only privileged accounts are authorized to run the preceding command.

-   Delete the pg\_cron plug-in.

    ```
    DROP EXTENSION pg_cron;
    ```

    **Note:** Only privileged accounts are authorized to run the preceding command.

-   Execute a scheduled task.

    ```
    SELECT cron.schedule('<Schedule>', '<Task>')
    ```

    Examples:

    ```
    -- Delete stale data at GMT 3:30 in the morning on every Saturday. 
    SELECT cron.schedule('30 3 * * 6', $$DELETE FROM events WHERE event_time < now() - interval '1 week'$$);
    
    ----------
    
    -- Clear disks at GMT 10:00 in the morning on every day.
    SELECT cron.schedule('0 10 * * *', 'VACUUM');
    
    ----------
    
    -- Execute the specified script once every minute.
    SELECT cron.schedule('* * * * *', 'select 1;');
    
    ----------
    
    -- Execute the specified script at the twenty-third minute of every hour.
    SELECT cron.schedule('23 * * * *', 'select 1;');
    
    ----------
    
    -- Execute the specified script on the fourth day of every month.
    SELECT cron.schedule('* * 4 * *', 'select 1;');
    ```

-   Execute a scheduled task on a specified database.

    ```
    SELECT cron.schedule('<Schedule>', '<Task>', '<Database>')
    ```

    **Note:** If you do not specify a database, the scheduled task is executed on the default postgres database that is specified in the configuration file.

-   Delete a scheduled task.

    ```
    SELECT cron.unschedule(<The ID of the scheduled task>)
    ```

    Example:

    ```
    SELECT cron.unschedule(43);
    ```

-   View all scheduled tasks.

    ```
    SELECT * FROM cron.job;
    ```

-   View the execution records of scheduled tasks.

    ```
    SELECT * FROM cron.job_log;
    ```


