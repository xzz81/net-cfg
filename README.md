# Sub Store Child - 家长控制订阅转换

通过 GitHub Actions 自动转换机场订阅，注入家长控制规则后生成 Shadowrocket 订阅链接。

## 设置步骤

### 1. 创建 GitHub 仓库

将此项目推送到 **私有仓库**（重要！防止订阅泄露）。

### 2. 添加订阅密钥

进入仓库 → Settings → Secrets and variables → Actions → New repository secret：

- Name: `SUB_URL`
- Value: `你的机场订阅链接`

### 3. 启用 GitHub Actions

进入 Actions 页面 → 启用 workflow → 手动运行一次 "Update Subscription"

### 4. 获取订阅链接

转换后的订阅文件位于：

```
https://raw.githubusercontent.com/你的用户名/仓库名/main/output/shadowrocket.txt
```

> 私有仓库需要用带 token 的链接：
> Settings → Developer settings → Personal access tokens → 生成一个只读 token
> 链接格式：`https://raw.githubusercontent.com/用户名/仓库名/main/output/shadowrocket.txt?token=你的TOKEN`
>
> 或者更简单：把仓库设为 public（订阅内容是加密的 base64，不含你的账号密码）。

### 5. 给孩子使用

Shadowrocket → 首页右上角 `+` → 类型 Subscribe → 粘贴上面的链接 → 保存

## 修改屏蔽规则

编辑 `rules/block_sites.list`，push 到 GitHub，Actions 会自动重新生成订阅。

## 自动更新频率

默认每 6 小时更新一次（可在 `.github/workflows/update-sub.yml` 中修改 cron）。
