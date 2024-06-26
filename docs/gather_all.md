## gather all命令

该命令用户收集集群的日志、observer所在主机的信息以及observer的堆栈信息

例子：
```shell script
 $ obdiag gather all -h
Usage: obdiag gather all [options]

Options:
  --from=FROM           specify the start of the time range. 'format: yyyy-mm-
                        dd hh:mm:ss'
  --to=TO               specify the end of the time range. 'format: yyyy-mm-dd
                        hh:mm:ss'
  --since=SINCE         Specify time range that from 'n' [d]ays, 'n' [h]ours
                        or 'n' [m]inutes. before to now. format: <n> <m|h|d>.
                        example: 1h.
  --scope=SCOPE         log type constrains, choices=[observer, election,
                        rootservice, all]
  --grep=GREP           specify keywords constrain
  --encrypt=ENCRYPT     Whether the returned results need to be encrypted,
                        choices=[true, false]
  --store_dir=STORE_DIR
                        the dir to store gather result, current dir by
                        default.
  -c C                  obdiag custom config
  -h, --help            Show help and exit.
  -v, --verbose         Activate verbose output.
```

例子：
```shell script

 $ obdiag gather all --from "2022-07-28 16:25:00" --to "2022-07-28 18:30:00" --encrypt true

...
ZipFileInfo:
+---------------+-----------+
| Node          | LogSize   |
+===============+===========+
| 192.168.2.11  | 29.874M   |
+---------------+-----------+
...

ZipFileInfo:
+----------------+-----------+
| Node           | LogSize   |
+================+===========+
| 192.168.2.12  | 143.229M  |
+----------------+-----------+
...


...
# 指定时间段内日志收集汇总
Summary:
+----------------+-----------+----------+------------------+--------+------------------------------------------------------------------------------------+
| Node           | Status    | Size     | Password         | Time   | PackPath                                                                           |
+================+===========+==========+==================+========+====================================================================================+
| 192.168.2.11   | Completed | 29.874M  | fB7FrrzTGl4EK5Hl | 20 s   | gather_pack_20220729170718/result_192.168.2.11_20220729222724_20220730003224.zip   |
+----------------+-----------+----------+------------------+--------+------------------------------------------------------------------------------------+
| 192.168.2.12   | Completed | 143.229M | SGRbXvMyA7lrnFW1 | 74 s   | gather_pack_20220729170718/result_192.168.2.12_20220729222724_20220730003224.zip   |
+----------------+-----------+----------+------------------+--------+------------------------------------------------------------------------------------+

...

# observer所在主机当前时间的主机信息收集汇总
Summary:
+----------------+-----------+---------+--------+----------------------------------------------------------------------+
| Node           | Status    | Size    | Time   | PackPath                                                             |
+================+===========+=========+========+======================================================================+
| 192.168.2.11   | Completed | 45.276K | 5 s    | gather_pack_20220729170856/sysstat_192.168.2.11_20220729170856.zip   |
+----------------+-----------+---------+--------+----------------------------------------------------------------------+
| 192.168.2.12   | Completed | 42.152K | 6 s    | gather_pack_20220729170856/sysstat_192.168.2.12_20220729170856.zip   |
+----------------+-----------+---------+--------+----------------------------------------------------------------------+


# observer当前的堆栈信息
Summary:
+----------------+-----------+---------+--------+-----------------------------------------------------------------------+
| Node           | Status    | Size    | Time   | PackPath                                                              |
+================+===========+=========+========+=======================================================================+
| 192.168.2.11   | Completed | 22.693K | 13 s   | gather_pack_20220729170902/obstack2_192.168.2.11_20220729170902.zip   |
+----------------+-----------+---------+--------+-----------------------------------------------------------------------+
| 192.168.2.12  | Completed | 19.902K | 13 s   | gather_pack_20220729170902/obstack2_192.168.2.12_20220729170902.zip    |
+----------------+-----------+---------+--------+-----------------------------------------------------------------------+

Gather Perf Summary:
+----------------+-----------+----------+--------+-------------------------------------------------------------------+
| Node           | Status    | Size     | Time   | PackPath                                                          |
+================+===========+==========+========+===================================================================+
| 192.168.2.11   | Completed | 368.178K | 90 s   | gather_pack_20230117140836/perf_192.168.2.11_20230117140836.zip   |
+----------------+-----------+----------+--------+-------------------------------------------------------------------+
| 192.168.2.12   | Completed | 368.178K | 90 s   | gather_pack_20230117140836/perf_192.168.2.12_20230117140836.zip   |
+----------------+-----------+----------+--------+-------------------------------------------------------------------+


```
