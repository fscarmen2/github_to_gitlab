# GitHub 到 GitLab 仓库同步工具

这个 GitHub Action 用于将 GitHub 上的仓库同步到 GitLab，确保 GitHub 上的最新变动被反映到对应的 GitLab 仓库。

## 功能

- 从 Cloudflare Worker 中获取所有的账户信息。
- 从 GitHub 仓库获取最新的 commit 信息。
- 比较 GitHub 和 GitLab 仓库的 commit 是否一致。
- 如果 GitHub 上有更新，将 GitHub 仓库的内容同步到 GitLab 仓库。

## 配置

通过 Cloudflare API，获取对应 worker 里的账户配置

## 使用说明

### 在 Cloudflare 面板创建可以读取 Worker 项目的 API, https://dash.cloudflare.com/profile/api-tokens

![image](https://github.com/user-attachments/assets/9e49b29a-54ae-46f0-aeda-28d95f4a9041)
![image](https://github.com/user-attachments/assets/11dceb4b-ab2e-41a8-b8e4-7317bcf4b50f)
![image](https://github.com/user-attachments/assets/b1e6f1c3-3d8d-4ba3-8d98-35ab4f061b14)
![image](https://github.com/user-attachments/assets/81e66642-cd5c-43d3-bb72-7fecf24e16a3)
![image](https://github.com/user-attachments/assets/3c832e81-bfc6-480d-939c-1d0731a07c17)

### 在 Action 处设置 3 个 secret 变量

![image](https://github.com/user-attachments/assets/25b8d0fa-8302-4cb9-a6db-83e449e9664c)

### Action yml 内容
```
name: Sync Repositories
on:
  schedule:
    - cron: '0 * * * *'  # 每小时运行一次
  workflow_dispatch:  # 允许手动触发

jobs:
  GitHub_To_GitLab:
    runs-on: ubuntu-latest
    env:
      ACCOUNT_ID: ${{ secrets.ACCOUNT_ID }}
      WORKER_NAME: ${{ secrets.WORKER_NAME }}
      API_TOKEN: ${{ secrets.API_TOKEN }}

    steps:
    - name: Checkout code
      uses: actions/checkout@v4.2.2

    - name: Clone Repo to GitLab
      continue-on-error: true
      uses: fscarmen3/github_to_gitlab@v1.0.1
```