# 课程实验

几门课的 lab 单独开了仓库，过程留在提交记录里。

## CSAPP

[csapp-labs](https://github.com/lvdousha26/csapp-labs)，C

CMU 15-213 的八个 lab：C 语言热身（队列 + 测试框架）、datalab 位运算、bomblab 拆炸弹、attacklab 缓冲区溢出、cachelab 缓存模拟与矩阵转置、shlab 带 job control 的 shell、malloclab 分配器、proxylab 带缓存的 HTTP 代理。

## JYY-OS

[jyyos-labs](https://github.com/lvdousha26/jyyos-labs)，C

南大蒋炎岩"操作系统"课的实验，主线是"程序如何并发、又如何变成操作系统"：`pstree` 打印进程树，`libco` 写用户态协程库，`crepl` 写一个 C 语言解释器，`kernel` 加上 `abstract-machine` 在裸机上跑起最小内核。

## CS336

[cs336-lab](https://github.com/lvdousha26/cs336-lab)，Python

Stanford CS336 *Language Modeling from Scratch*，五个 assignment 都留了 writeup：

1. basics：BPE 分词器、Transformer、AdamW、训练循环
2. systems：Triton kernel，DDP / FSDP / 张量并行
3. scaling：Chinchilla 拟合与 IsoFLOP 曲线
4. data：Common Crawl 抽取、质量过滤、去重
5. alignment：SFT、DPO、RLHF（另有一份安全方向的补充）
