# Cloudflare Worker 反代工具

本项目是一个基于 Cloudflare Workers 的反向代理工具，参考自 [CSDN 博客](https://blog.csdn.net/weixin_60451356/article/details/136106548)。

## 功能简介

- 支持通过 Cloudflare Workers 实现反向代理
- 可自定义 PC 和移动端代理目标地址（通过 `upstream` 和 `upstream_mobile`）
- 支持访问区域和 IP 黑名单
- 支持路径和域名替换
- 自动将 HTTP 请求重定向到 HTTPS
- 自动设置 CORS 相关响应头

## 使用方法

1. **部署到 Cloudflare Workers**

    - 进入 [Cloudflare Workers 控制台](https://dash.cloudflare.com/)。
    - 新建一个 Worker，将本项目的 `worker.js` 代码粘贴进去。

2. **配置代理参数**

    在 `worker.js` 顶部手动设置你的目标代理地址，例如：

    ```js
    // 反代目标网站
    const upstream = "github.com"; // 这里填写你要反代的主站域名
    // 反代目标网站的移动版
    const upstream_mobile = "github.com"; // 这里填写你要反代的移动版域名，如无可与主站相同
    ```
    
    如需自定义黑名单、替换规则等，也可在对应变量处修改：
    - `blocked_region`：访问区域黑名单
    - `blocked_ip_address`：IP 黑名单
    - `replace_dict`：路径/域名替换规则

3. **保存并部署**

    - 点击“保存并部署”按钮。
    - 访问分配给你的 Worker 域名，即可通过 Worker 实现反向代理。

## 注意事项

- 请勿用于非法用途。
- 根据目标站点的 robots.txt 和相关政策合理使用。
- 如需屏蔽特定地区或 IP，可修改 `blocked_region` 和 `blocked_ip_address`。
- 如需自定义路径替换规则，可修改 `replace_dict`。
