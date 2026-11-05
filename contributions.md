# Open Source

Small PRs, each fixing one concrete behavior.

## vLLM

[vllm-project/vllm#58072](https://github.com/vllm-project/vllm/pull/58072), open

`Phi4MiniJsonToolParser` returns `tools_called=True` as soon as it sees a `functools[...]` marker, but two payloads parse to nothing: `functools[]` becomes an empty list after `json.loads`, and `functools[ some plain text ]` raises, gets logged, and is swallowed, leaving the accumulator empty. Both fall through to the success return, so the parser reports a tool call that does not exist and sets `content` to `None`, dropping the text it should have passed through.

The fix returns `tools_called=False` with the output left in `content` when nothing was parsed, adds a test for it, and removes the matching "empty array is misreported" entry from the known-failure config.

## cs-self-learning

[PKUFlyingPig/cs-self-learning#916](https://github.com/PKUFlyingPig/cs-self-learning/pull/916), draft

The site mounts giscus with `data-mapping="title"`, so a page's thread is looked up through issue search on the title. That search is tokenized and fuzzy: rename a page and its thread is orphaned for good, and two pages whose titles share tokens end up rendering each other's comments. Both are real here — two pages currently share a title. Switching to `pathname` + `strict` takes two lines, but the existing discussions have to be migrated first, otherwise every page renders zero comments. Hence the draft.

## Open-Source-Dashboard

[hust-open-atom-club/Open-Source-Dashboard](https://github.com/hust-open-atom-club/Open-Source-Dashboard), 2 merged / 2 closed / 1 open

The club's community dashboard (React + FastAPI). Merged: the CI actions bumped to the native Node 24 runtime, and dialog semantics plus focus handling for the three detail modals — `role="dialog"`, `aria-modal`, a label pointing at the heading, focus moved to the close button on open and restored to the trigger on close.

Two smaller ones (keyboard access on the leaderboard, the local Vite port) were not taken. #86, a SIG selector for the multi-SIG trend chart, is still in review.

## HelloAgents

[jjyaoao/HelloAgents#116](https://github.com/jjyaoao/HelloAgents/pull/116), open

qdrant-client 1.16.0 removed `CollectionInfo.vectors_count`. `QdrantVectorStore.get_collection_info()` read that field directly, so the `AttributeError` was raised, swallowed by the surrounding `except Exception`, and `get_collection_stats()` came back as an empty dict — every statistic gone, plus one failure log per call. Replaced with `getattr` fallbacks (a single unnamed vector collection can fall back to `points_count`), checked on 1.15.1 / 1.16.0 / 1.19.1.

## LLaMA-Factory

[hiyouga/LlamaFactory#10934](https://github.com/hiyouga/LlamaFactory/pull/10934), merged

Three README paths that no longer resolve, in both the English and Chinese files. `examples/requirements/` moved to the repo root in v0.9.5, so the install command fails — the sentence right above it already uses `requirements/metrics.txt`. The changelog entry for the OpenAI-compatible API still names `src/api_demo.py`, now `src/api.py`. And `Qwen/Qwen2-Audio-7B-Instruct` had no scheme, so GitHub resolved it as a directory inside LLaMA-Factory rather than a model on Hugging Face.
