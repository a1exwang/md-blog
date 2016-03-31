# Bash cheatsheet

- tags: bash, one-line script

* * *

##### Reference: https://github.com/jlevy/the-art-of-command-line

- 快捷键
  - alt-b, alt-f, 左右移动一个单词
  - ctrl-w 删除最后一个单词
  - ctrl-k 删除光标之后的所有内容

- file system
  - cd -
    - 回到上一个目录
  - ls -al
  - pv (monitor the progress of data through a pipe)
    - -b(display bytes)
    - -r(display rate)
  - stat查看文件属性
    - 可以显示文件的设备号
  - lsof (LiSt Open Files)列出打开的文件
    - sudo lsof file_path, 列出打开了file_path文件的进程

- file
  - du (estimate file space usage)
    - -h (Human-readable)
    - --max-depth=N
  - df (show Disk usage)
    - -h (Human-readable)
  - file (show file type)
  - `<(some command)` 可以将输出视为文件。例如，对比本地文件 /etc/hosts 和一个远程文件：
      `diff /etc/hosts <(ssh somehost cat /etc/hosts)`

- device
  - lsblk 列出block device, 一般是硬盘驱动器

- process
  - strace:监视进程的系统调用
    - -e trace=file, 仅监视参数中有文件位置的系统调用

  - pgrep 按照进程名grep
    - -l列出pid和进程名
  - nohup 启动进程忽略挂起信号(当用户logout时发出)

- job
  - Ctrl+Z (stop current task)
    - bg (switch task 1 to BackGround)
    - fg (switch task 1 to ForeGround)
    - kill %1 (kill task 1)

- text
  - tail
    - -n NUM
    - -f (update file content)
  - 生成随机字符串
    - head /dev/urandom | tr -dc A-Za-z0-9 | head -c10
  - sort
    - -n 将每行当成数字排序,
    - -h 将每行当成文件大小排序(e.g. 10K, 100M)
    - -M 按照日期排序
    - e.g.
      - `find . -type f -exec du -ah {} + | sort -h | tail -10`列出当前目录树下最大的几个文件
      - `cat /var/log/nginx/access.log | cut –d " " -f 1 | sort| uniq | wc -l `列出服务器的独立访问IP
  - grep -A -B -C 多显示几行

- network
  - netstat
    - -anop | grep 1234, 列出占用1234端口的进程
  - dig
  - rsync -azP --exclude=.git . alexwang@166.111.227.241:/home/alexwang/llvm
    - 快速将本地的项目同步到服务器, -a增量传输, -z压缩传输, -P打印过程
- misc
  - 特殊变量
    - $? 上一个命令的返回值
  - apropos
    - 查找文档
