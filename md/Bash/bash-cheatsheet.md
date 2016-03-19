# Bash cheatsheet

- tags: bash, one-line script

* * *

- ls -al
- pv (monitor the progress of data through a pipe)
  - -b(display bytes)
  - -r(display rate)
- Ctrl+Z (stop current task)
  - bg (switch task 1 to BackGround)
  - fg (switch task 1 to ForeGround)
  - kill %1 (kill task 1)
- du (estimate file space usage)
  - -h (Human-readable)
  - --max-depth=N
- df (show Disk usage)
  - -h (Human-readable)
- file (show file type)

- tail
  - -n NUM
  - -f (update file content)

- netstat
  - -anop | grep 1234, 列出占用1234端口的进程
- 特殊变量
  - $? 上一个命令的返回值
