# 🌍 Cloudflare Worker 任意网站反向代理（优选域名方案）

基于 **Cloudflare Workers + Worker Routes** 实现的通用反向代理方案。  
通过「子域名前缀映射」的方式，将多个子域名自动反代到不同源站，实现优选域名、隐藏源站、统一 HTTPS、添加 CORS 等功能。

---

## ✨ 功能特性

- ✅ 支持多个源站映射
- ✅ 基于子域名前缀自动匹配
- ✅ 强制 HTTPS
- ✅ 自动重写 Host / Referer
- ✅ 添加 CORS 头
- ✅ 移除 CSP 限制（可嵌入）
- ✅ 可配合 Worker 路由实现泛域名优选

---

## 🏗️ 工作原理

例如：

```js
const domain_mappings = {
  'gitea.072103.xyz': 'gitea.',
};
```

当你设置 Worker 路由为： `gitea.*`

那么：

```
gitea.abc.com  →  gitea.072103.xyz
gitea.test.com →  gitea.072103.xyz
```

## 逻辑流程

- 获取当前访问 Host
- 提取匹配的前缀
- 根据前缀查找源站域名
- 构造新的请求
- 透传响应并修改响应头
