# 静态隐私与支持网站草稿

这里是可直接交给静态托管的网页，没有业务后台、JavaScript、表单、Cookie、统计代码、远程字体或外链资源。不需要开发者自建业务服务器；HTTPS 静态托管仍由服务商提供网页，并可能产生访问日志。当前没有发布公网，也没有公开网站或 App Store 下载链接。

## 文件与维护

- `index.html`：产品首页；说明本机归档、比较指标、可选第三方 AI 与长期免费下载。没有虚构机构或医学数据示例。
- `privacy.html`：由 `../../privacy-policy.md` 生成的用户隐私正文。
- `support.html`：公开邮箱、常见问题与删除／备份说明。
- `styles.css`：三页共用的本地样式，适配手机和 iPad／桌面。
- `site-config.json`：发布资料清单，当前 `status=draft`。它不在浏览器执行，也不会自动替换首页或支持页文案。
- `build_privacy.py`：Python 标准库本地构建工具，只生成 `privacy.html`，不发网络请求。

目前公开支持和隐私邮箱已获用户授权：`martinyun@gmail.com`。Gmail 在中国大陆的访问、收发及本人持续处理邮件的可用性仍需本人验证；可以再提供一个稳定公开渠道写入 `backupContact`，目前不编造备用地址。开发者实名尚未提供，使用“HealthArchive 个人开发者，身份以发布时 App Store 开发者信息为准”，不能虚构姓名、地址、公司或固定回复时限。

无网页统计不等于托管方无访问日志。例如 [GitHub Pages 官方说明](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages#data-collection)明确其会为安全目的记录访客 IP。它只是边界说明，不代表已选择 GitHub 托管；最终仍由用户确认大陆可访问的静态托管方案，再核对该托管方的实际规则。

修改政策先改 `docs/privacy-policy.md`，然后在仓库根执行：

```sh
python3 docs/release/website/build_privacy.py
git diff --check
```

如改变网站联系方式、日期或发布状态，同时同步配置、三个页面页脚、支持页及政策。构建器只适用于这里使用的段落、二级标题和简单项目列表，不是通用 Markdown 处理器。不要向 Markdown 放入 HTML 或未知格式。

## 本地预览

在仓库根打开一个独立终端运行，只监听本机：

```sh
python3 -m http.server 8769 --bind 127.0.0.1 --directory docs/release/website
```

浏览器打开 `http://127.0.0.1:8769/index.html`、`privacy.html` 和 `support.html`。检查 320／390 像素手机宽度、iPad 宽度、键盘焦点、隐私段落与 FAQ 展开；完成后在该终端按 Control-C。这个临时预览服务不是产品后台，不上传健康资料。不要使用 `0.0.0.0` 或端口转发来代替正式发布。

## 正式静态上传前

### 没有域名时的免费预发布路径

如果决定先用 GitHub Pages，用户在 GitHub 新建一个**独立的公开网站仓库**，只上传下文的四个运行文件到仓库根目录。在 Settings → Pages → Build and deployment 选择 Deploy from a branch，选择实际分支及 `/(root)` 后保存。等待 Pages 显示真实站点 URL；不要把示例占位 URL 填入 App。

免费公共仓库可托管静态网页，默认地址由本人账号和实际仓库名决定。先用大陆移动网络和 Wi-Fi 验证首页、隐私、支持均无需登录可读，再判断是否适合作为长期支持网址。需要更稳定的大陆访问时，再考虑真实自有域名与合规境内静态托管；不会因此需要接收病历的服务器。网站托管不替代 App ICP／AI 功能适用核验。具体创建步骤见 [GitHub 官方说明](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)。

本轮 [website-draft.zip](../website-draft.zip) 只打包这四个静态文件，保留草稿提示，供查看和后续正式填写。未公开上传。确定身份、托管规则和生效日期、修改正文后应重新打包；不要直接把未填写的草稿当成生效政策。

### 公开发布检查

1. 核对与 App Store 一致的个人开发者身份，填写配置中的 `developerLegalName`；按最终公开身份更新政策。无需在网页公开未要求提供的家庭地址。
2. 用户确认静态托管方案与一个长期有效的 HTTPS 公开地址，填写 `publicBaseURL`、托管方、数据地区和访问日志规则。选择服务后核对大陆可访问性，不以本机预览成功代替公网验证。
3. 为托管日志填写明确处理目的、保留期限和删除渠道，替换政策第9节“尚未公开托管”的草稿文字。不要保证托管商永不记录 IP，除非有实际配置与合同依据。
4. 确认政策生效日期，同步各页日期。由本人验证 Gmail 在大陆可访问、能收发并持续处理隐私请求；如不可用，先提供并公开稳定备用渠道。不要通过测试邮件发送病历或密钥，也不承诺快速响应。
5. 核对是否仍无广告／统计／遥测 SDK、账号和业务后台。若未来实现非消耗型内购，应先补交易数据与恢复购买说明；当前不能声称已经实现 StoreKit 或购买能力。
6. 用户明确授权发布后，移除三个页面的草稿条幅、页脚“发布草稿”以及 `robots=noindex,nofollow`，并同步构建器模板，防止再次生成草稿。设置 `status=ready` 本身不会完成这些修改。
7. 只上传 `index.html`、`privacy.html`、`support.html`、`styles.css`。不要上传整个仓库、`.build/`、`output/`、报告、凭据、配置清单或本地构建脚本。配置需要由维护者保存，网页运行不需要它。
8. 发布后逐一验证三页及 CSS 返回成功、HTTPS 有效、无需登录、没有外部请求、手机排版完整、邮箱链接有效。托管如支持，可设置 `Content-Security-Policy: default-src 'none'; style-src 'self'; img-src 'self'; base-uri 'none'; form-action 'none'; frame-ancestors 'none'`、`Referrer-Policy: no-referrer`、`X-Content-Type-Options: nosniff`。页面内的 CSP 不能代替所有响应头设置。
9. 将实际 `…/privacy.html`、`…/support.html` HTTPS URL 交回 App 的公开链接配置和 App Store Connect，再做最终隐私问卷核对。当前资料不是已通过审核的声明。

## 源码核对依据（2026-10-06）

| 已确认的流 | 仓库依据 |
| --- | --- |
| 仅本机结构化库、关闭 CloudKit、文件保护及排除自动备份 | `HealthArchive/MyApp/MyApp.swift`、`Services/DocumentImportService.swift` |
| OCR 不发网络 | `Services/OCRService.swift`，使用本机 Vision 文字识别 |
| 密钥读写与清除、只保存在系统钥匙串 | `Services/ModelParsingService.swift` 的 `KeychainAPIKeyStore`、`Services/LLMConfigurationStore.swift` |
| HTTPS 用户配置地址、阻断重定向、无开发者转发 | `Services/AIEndpointResolver.swift`、`Services/AIModelTransport.swift` |
| 发送同意及所选范围 | 报告发送确认页、`Views/JournalView.swift`、`Views/ArchiveQueryView.swift`、归类复核及核对修复视图／服务 |
| 本机使用历史不含正文或密钥、删除报告解除历史关联 | `Models/AIRequestRecord.swift`、`Services/AIUsageStore.swift` |
| 报告删除、共享原件剩余引用与失败恢复 | `ContentView.swift` 的报告删除、`Views/JournalView.swift` 的健康记录删除 |
| ZIP 备份不含模型配置／Key，恢复不调模型 | `Services/PortableArchiveService.swift`、`Services/PortableArchiveSnapshot.swift`、`Views/BackupRestoreView.swift` |
| 无第三方依赖、账号、广告、分析 SDK、遥测、StoreKit 交易实现 | 工程依赖、App 源码关键字与联网路径、`PrivacyInfo.xcprivacy`；此结论只针对当前版本，新增功能必须重新核对 |

网页正文刻意不包含数据库表名、本地私有路径、接口 DTO 等实现细节。支持邮件是用户主动联系后的单独资料处理，不属于 App 自动遥测。

Apple 要求隐私政策说明资料用途、第三方处理、保留与删除、撤回同意，并在 App 内和商店元数据提供易访问链接；这不表示本草稿已通过审核。[App Review Guidelines 5.1.1](https://developer.apple.com/app-store/review/guidelines/#privacy)。未来非消耗型内购是一次购买、不因使用而耗尽的类型，实际交易实现仍需另做。[Apple 内购类型说明](https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/overview-for-configuring-in-app-purchases)。这些官方链接只在维护说明中，不是公开网页加载的资源。
