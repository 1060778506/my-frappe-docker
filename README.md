Frappe/ERPNext v15 多应用集成镜像构建工具
🚀 项目简介
本项目基于 GitHub Actions，通过对 Frappe 官方 layered 构建镜像进行“手术级”逻辑注入，实现了在 Docker 构建过程中自动集成 ERPNext、HRMS、Insights 以及多个自定义第三方 App 的全自动流水线。

🛠️ 核心突破：解决官方 v3.0.0 构建限制
在官方 frappe_docker v3.0.0 更新后，传统的环境变量传参安装 App 的方式失效。本项目通过以下技术手段破解了该限制：

物理补丁注入：动态生成 apps.json 配置文件并强制 COPY 进入构建环境。

图纸自动化修补：利用 sed 指令实时修改官方 Containerfile，绕过 Secret 挂载限制。

全局环境锁定：自动修复多阶段构建中的变量丢失问题，确保构建 100% 成功。

国内环境优化：预置 NPM/Yarn 国内镜像源及 Git 缓冲区优化，大幅提升构建速度。

📦 已集成的应用清单
镜像在构建时会自动拉取并安装以下应用（版本保持同步更新）：

应用名称	说明	来源
Frappe	核心底层框架	官方 GitHub
ERPNext	企业资源规划核心	官方 GitHub
HRMS	人力资源管理模块	官方 GitHub
CRM	客户关系管理	官方 GitHub
Insights	数据分析报表工具	官方 GitHub
Fengjing App	自定义业务模块	私有/自定义仓库
ERPNext China	中国化增强插件	Gitee 镜像
Other Apps	打印设计、雪铲工具、Wiki等	社区及自研
🏗️ 构建流程说明
本项目流水线（CI/CD）逻辑如下：

环境初始化：拉取最新的官方 Docker 施工图纸。

手术注入：

动态注入管理员权限。

在特定层级插入 apps.json 扫描指令。

追加 Insights SSL 修复补丁（自动关闭数据库证书强制校验）。

多仓推送：构建完成后同步推送到 Docker Hub 及 阿里云容器镜像服务 (杭州节点)。

自动校验：构建末尾自动运行 bench version 确认所有应用安装状态。

🚦 使用指南
1. 变量配置
请在 GitHub 仓库的 Settings > Secrets and variables > Actions 中配置以下密钥：

DOCKERHUB_USERNAME / DOCKERHUB_TOKEN

ALIRP_USERNAME / ALIRP_PASSWORD (阿里云凭据)

2. 版本管理
注意：本项目采取 动态版本策略。

内核版本：跟随 Frappe 官方 version-15 分支实时演进。

应用版本：在 workflow.yml 的 apps.json 段落中定义。如需升级特定 App，只需修改对应的 branch 或 tag 即可，无需重写构建逻辑。

3. 手动触发
进入 GitHub Actions 页面，选择 Frappe-v15-多应用全家桶构建，点击 Run workflow 即可开始全量无缓存构建。

⚖️ 许可证
基于 MIT License 开源。本项目所有逻辑均针对 Frappe 官方构建脚本进行兼容性适配。
