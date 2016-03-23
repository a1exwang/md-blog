# Bash cheatsheet

- tags: bash, one-line script

* * *

- Legal

![Creative Commons License 3.0](CC.png "CC 3.0")


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
- 生成随机字符串
  - head /dev/urandom | tr -dc A-Za-z0-9 | head -c10
- sort
  - -n 将每行当成数字排序,
  - -h 将每行当成文件大小排序(e.g. 10K, 100M)
  - -M 按照日期排序
  - e.g.
    - `find . -type f -exec du -ah {} + | sort -h | tail -10`列出当前目录树下最大的几个文件
    - `cat /var/log/nginx/access.log | cut –d " " -f 1 | sort| uniq | wc -l `列出服务器的独立访问IP
- strace:监视进程的系统调用
  - -e trace=file, 仅监视参数中有文件位置的系统调用
- stat查看文件属性
  - 可以显示文件的设备号
