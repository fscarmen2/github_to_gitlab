# GitHub 到 GitLab 仓库同步工具

这个 GitHub Action 用于将 GitHub 上的仓库同步到 GitLab，确保 GitHub 上的最新变动被反映到对应的 GitLab 仓库。

## 功能

- 从 GitHub 仓库获取最新的 commit 信息。
- 比较 GitHub 和 GitLab 仓库的 commit 是否一致。
- 如果 GitHub 上有更新，将 GitHub 仓库的内容同步到 GitLab 仓库。

## 配置

在使用之前，你需要创建一个配置文件 `config.yml`，并确保将其路径传递给 `config_path` 参数。配置文件需要包含以下内容：

## 使用说明
```
    - name: Clone Repo to GitLab
      uses: fscarmen2/github_to_gitlab@v1.0.0
      with:
        config_path: < 用户配置文件存放路径，不填则默认: ./config.yml >
```