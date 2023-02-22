---
creation date: 2023-01-31 21:46
modification date: Tuesday, 31st January 2023, 21:46:45
tags: today_i_leaned
---

# Working and debugging systemD



```bash
# Reload systemctl after changing a service
systemctl daemon-reload

# View service status
systemctl status <servicename>

# View log of a specific service
journalctl -u <servicename>.service

```

View **journalctl** without PagingPermalink To send your logs to standard output and avoid paging them, use the --no-pager option:

`journalctl --no-pager`

It’s not recommended that you do this without first filtering down the number of logs shown.

`journalctl -u <servicename>.service`

Show Logs within a Time RangePermalink Use the --`since` option to show logs after a specified date and time:

`journalctl --since "2018-08-30 14:10:10"`

Use the --until option to show logs up to a specified date and time:

`journalctl --until "2018-09-02 12:05:50"`

Combine these to show logs between the two times:

`journalctl --since "2018-08-30 14:10:10" --until "2018-09-02 12:05:50"`

---
#### references
https://www.linode.com/docs/guides/how-to-use-journalctl/