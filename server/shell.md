# 命令与Shell

## 常用命令

**查看进程堆栈**

`pstack <pid>`

`gstack <pid>`

```bash
gdb
attach <pid>
thread apply all bt
```

**脱离Shell执行**

```bash
nohup docsify serve /vis/doc/ < /dev/null > /dev/null 2>&1 &
disown
```
