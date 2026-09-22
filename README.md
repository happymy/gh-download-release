# gh-download-release

从 `urls.txt` 中逐行读取下载地址，自动下载文件并发布到 GitHub Release。

## 工作流程

GitHub Actions 工作流（`.github/workflows/download-and-release.yml`）触发方式：

- **手动触发**：Actions 页面点击 `Run workflow`
- **自动触发**：当 `urls.txt` 有变更并提交推送后自动运行

### 执行步骤

1. 读取 `urls.txt`，逐行下载每个 URL（跳过空行与 `#` 注释行）
2. 将下载成功的文件作为资产发布到新建的 GitHub Release
3. 仅从 `urls.txt` 中清除下载成功的地址（保留失败地址与 `#` 注释行）并提交推送

## 使用说明

1. 在 `urls.txt` 中填写要下载的地址，每行一个：

```
# 示例（注释会被保留，运行后不删除）
https://example.com/file1.zip
https://example.com/file2.zip
```

2. 提交并推送，或在 Actions 页面手动触发工作流
3. 完成后下载的文件可在仓库的 **Releases** 页面找到
4. `urls.txt` 中的地址会自动清空，可继续填写下一批

## 注意

- 某地址下载失败：该地址留在 `urls.txt`，不阻塞其余地址下载与发布，可修复后重跑
- 若 Release 发布失败，`urls.txt` 中全部地址保留，可修复后重跑
- 仅下载成功且 Release 发布成功后的地址会被清除

## 许可证

[MIT](./LICENSE)