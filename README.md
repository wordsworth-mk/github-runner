# README

仓库 60d 没动静，流水线会自动暂停（会有邮件通知）

## 为什么会被暂停

GitHub 的规则：**public 仓库连续 60 天没有任何活动（提交/推送）时，所有 `schedule:` 触发的 workflow 会被自动禁用**（状态变为 `disabled_inactivity`），并发送邮件通知。

参考：[Disabling and enabling a workflow](https://docs.github.com/en/actions/how-tos/manage-workflow-runs/disable-and-enable-workflows)

本仓库目前只有 [`05.app_checkin.yml`](.github/workflows/05.app_checkin.yml) 使用了 `schedule:`，其余都是手动 / `dispatch` 触发，因此此前只有它被暂停。

## 如何防止

[`00.repo_keep_alive.yml`](.github/workflows/00.repo_keep_alive.yml) 每 5 天自动运行一次，做两件事：

1. 往 `main` 推一个空提交（`chore: keepalive [skip ci]`），刷新仓库活跃时间，让 60 天计时器永远走不到头；
2. 扫描所有处于 `disabled_inactivity` 状态的 workflow 并重新启用（自愈，双保险）。

也可以手动触发：

```bash
gh workflow run "00. 💓 repo_keep_alive"
```

或由外部定时器通过 `repository_dispatch`（`type: keep_alive`）唤醒。

## 手动恢复被暂停的流水线

```bash
# 查看所有 workflow 的状态（含被禁用的）
gh workflow list --all

# 重新启用被自动禁用的 workflow
gh workflow enable "05. ✅ app_checkin"
```

> 只要 keep-alive 正常工作（仓库始终有提交活动），就不需要手动恢复。
> 若发现空提交没有算作仓库活动（极少见），可改用带 `contents: write` 的 PAT 来 push，或直接用外部定时器触发本 workflow。
