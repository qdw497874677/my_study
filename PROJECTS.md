# 项目说明

本仓库包含多个学习项目的记录。

## 子项目仓库状态

本仓库中的部分子目录包含独立的 `.git` 仓库，这是为了支持 OpenCode 将这些目录识别为独立项目进行管理。

### study_of_web3/
- 包含独立 `.git` 仓库
- 同时在本仓库跟踪部分文件内容
- 内容：Web3 深度学习项目

### study_of_ai_coding/
- 包含独立 `.git` 仓库
- 同时在本仓库跟踪部分文件内容
- 内容：AI 编程分享大纲、Agents 文档

## 提交时注意事项

由于子目录存在独立 `.git` 仓库，添加文件时需分别添加具体文件，而非整个目录：
```bash
git add study_of_ai_coding/AGENTS.md study_of_ai_coding/ai-coding-sharing-outline.md
```
