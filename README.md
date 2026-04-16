





🛠️ 核心突破：解决官方 v3.0.0 构建限制

针对官方 frappe_docker v3.0.0 版本后的构建机制变化，本项目通过以下技术手段确保构建成功：

物理清单注入：动态生成 apps.json 配置文件并强制 COPY 进入构建环境，绕过了复杂的 Secret 挂载限制。

图纸自动化修补：利用 sed 指令实时修改官方 Containerfile，自动修复多阶段构建中的变量丢失问题。

国内环境优化：预置 NPM/Yarn 国内镜像源及 Git 缓冲区优化，大幅提升构建速度。

数据库 SSL 修复：自动识别并修补 Insights 应用的数据库连接逻辑，关闭强制 SSL 验证。






📦 已集成的应用清单
ERPNext (v15.104.3)：核心企业资源规划系统。

HRMS (v15.59.0)：人力资源与薪资管理系统。

Frappe CRM (v1.67.1)：客户关系管理系统。

Insights (v3.8.0)：商业智能与数据报表分析工具。

Fengjing App (develop)：你的自定义业务模块。

ERPNext China (master)：ERPNext 的中国本地化增强插件。

Beam (v15.10.0)：农场/农业管理相关扩展。

Print Designer (v1.6.7)：强大的打印格式可视化设计器。

Builder (v1.23.2)：网页与界面可视化构建工具。

Wiki (master)：企业内部知识库/维基应用。

Crispy Print (develop)：增强型打印/排版工具插件。
