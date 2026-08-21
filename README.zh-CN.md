# zjy365 Skills

一组可直接安装使用的 Agent skills，适用于 Codex 和其他支持 [skills.sh](https://skills.sh/) 的工具。

[English README](README.md)

## 能做什么

| Skill | 适合什么 |
| --- | --- |
| `ui-router` | 根据 UI 任务选择合适的设计、实现、重构、动效、无障碍和质量检查 skills。 |
| `mole` | 在 macOS 上分析磁盘、检查系统状态、清理缓存、卸载应用和释放空间。删除操作会先预览，并等待确认。 |
| `objective-crafter` | 把粗略想法整理成可执行的 Codex `/goal`，补齐目标、验收方式、约束和停止条件。它只写 Goal，不直接执行任务。 |

## 安装

```bash
npx skills add zjy365/skills
```

## 使用

安装后，直接用自然语言描述任务，也可以明确指定 skill。

选择 UI skills：

```text
使用 $ui-router，帮我判断这个 SaaS 后台重构应该先用哪些 UI skills。
```

安全检查和清理 Mac：

```text
使用 $mole，检查我的 Mac 哪些内容可以安全清理。先给我预览，暂时不要删除。
```

整理可执行目标：

```text
使用 $objective-crafter，把“把这个项目做得更快”整理成一个可验证的 /goal。
```

## 常用命令

查看已安装的 skills：

```bash
npx skills list
```

更新 skills：

```bash
npx skills update
```

移除 skills：

```bash
npx skills remove
```

## 安全说明

`mole` 只支持 macOS。清理、卸载或修改系统前，它会先生成预览，并等待你确认具体方案。清理操作的确认不会自动授权永久删除或其他高风险操作。
