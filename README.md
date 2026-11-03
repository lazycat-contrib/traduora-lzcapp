# Traduora 懒猫微服包

自托管翻译管理平台：词条、语言与译文集中维护。

- 上游：<https://github.com/ever-co/ever-traduora>
- 镜像：`everco/ever-traduora`
- 许可：AGPL-3.0（全文见 content/licenses/LICENSE）

## 组成

| 服务 | 镜像 | 作用 |
| --- | --- | --- |
| `traduora` | `everco/ever-traduora` | 应用本体，监听 8080 |
| `db` | `postgres:15-alpine` | 数据库 |

## 关键配置说明

- **管理员账号由环境变量预置**：`TR_ADMIN_EMAIL` / `TR_ADMIN_PASSWORD` / `TR_ADMIN_NAME`。
  上游文档明确：`TR_ADMIN_PASSWORD` **必填且无默认**，并且**会拒绝公开已知的旧默认密码**。
  本包用部署参数生成随机强密码。
- `TR_SECRET` 用稳定密钥，变化会让所有人被登出。
- DSN 相关密码用十六进制编码，避免特殊字符破坏连接串。
- 应用自带账号体系，因此开放 `public_path`，由应用自己鉴权。
- 未配置 SMTP：邀请成员等发信功能需自行配置邮件服务。

## 未验证部分

未在真机上实测：登录、创建项目与语言、编辑译文、导出文件、重启后数据留存。
