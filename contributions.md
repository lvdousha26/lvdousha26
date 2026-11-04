# 开源贡献

提的 PR 都不大，基本是修一个具体的行为问题。按项目记一下。

## vLLM

[vllm-project/vllm#58072](https://github.com/vllm-project/vllm/pull/58072)，待合并

`Phi4MiniJsonToolParser` 只要见到 `functools[...]` 标记就返回 `tools_called=True`，但有两种 payload 解析出来是空的：`functools[]` 被 `json.loads` 读成空列表，`functools[ 一段普通文本 ]` 解析失败后异常被日志吞掉、累加器仍是空的。两种情况都落到成功分支，于是报出一个并不存在的 tool call，`content` 给成 `None`，本该原样返回的文本也一起丢了。

改成解析结果为空时返回 `tools_called=False`、把输出放回 `content`，并补了一条用例，同时删掉测试配置里"空数组会误报"那条已知失败项。

## cs-self-learning

[PKUFlyingPig/cs-self-learning#916](https://github.com/PKUFlyingPig/cs-self-learning/pull/916)，draft

站点用 giscus 挂评论，配置是 `data-mapping="title"`，也就是线程靠标题搜索来匹配。标题搜索本身是分词后的模糊匹配：改一次标题，旧线程就失联；标题撞词的两页还会互相渲染对方的评论——站上现在确实有两页同名。换成 `pathname` + `strict` 只要两行，但得先把已有讨论迁移过去，否则所有页面会显示零评论，所以先挂成 draft 等顺序。

## Open-Source-Dashboard

[hust-open-atom-club/Open-Source-Dashboard](https://github.com/hust-open-atom-club/Open-Source-Dashboard)，2 merged / 2 closed / 1 open

学校开源俱乐部的社区看板（React + FastAPI）。合并的两条：把 CI 的 Actions 升到原生 Node 24 运行时；给贡献者、日期、仓库三个详情弹窗补上 `role="dialog"`、`aria-modal`、标题关联，以及打开时聚焦关闭按钮、关闭后焦点回到触发元素。

另有两个键盘可达性、本地 Vite 端口的小改动没进；#86 给多 SIG 趋势图加选择器还在 review。

## HelloAgents

[jjyaoao/HelloAgents#116](https://github.com/jjyaoao/HelloAgents/pull/116)，待合并

qdrant-client 1.16.0 移除了 `CollectionInfo.vectors_count`，`QdrantVectorStore.get_collection_info()` 读这个字段会抛 `AttributeError`，又被方法里的 `except Exception` 吞掉，`get_collection_stats()` 于是返回空字典，统计字段全丢，每次调用还多打一条失败日志。改成 `getattr` 兜底（单无名向量集合用 `points_count` 等价回退），1.15.1 / 1.16.0 / 1.19.1 三个版本都跑过。
