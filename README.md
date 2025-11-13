    <strong>一款全新的主动资产指纹识别工具</strong>
</p>

<p align="center">
    <a href="https://github.com/yourusername/muki/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg"></a>
    <a href="https://github.com/yourusername/muki/releases"><img src="https://img.shields.io/github/v/release/yourusername/muki"></a>
    <a href="https://golang.org/"><img src="https://img.shields.io/badge/language-Go-blue.svg"></a>
</p>
</p>
<p align="center">
  <img width="364" height="150" alt="Muki - Active Asset Fingerprinting Tool" src="https://github.com/user-attachments/assets/fd331a9e-7628-462e-9189-3eb8387323c6" />
</p>
<p align="center">
Muki 是一款专为红队作战设计的主动资产指纹识别工具。在信息收集阶段，Muki 能够帮助安全研究人员快速从 C 段、大量杂乱的资产中精准定位到易被攻击的系统，从而实施进一步的渗透测试。

Muki is a brand-new active asset fingerprinting tool designed for red team operations. During reconnaissance, Muki enables security researchers to rapidly pinpoint vulnerable systems from chaotic C-class segments and massive asset lists, enabling targeted exploitation.

---

## ✨ 特性

- **代理池支持**：支持从文件加载多个代理地址，自动轮换使用，避免 IP 限制  
  **Proxy Pool Support**: Load multiple proxy addresses from file with automatic rotation to avoid IP blocking

- **智能去重**：基于 URL 标准化的高级去重算法，显著提高扫描效率  
  **Smart Deduplication**: Advanced deduplication algorithm based on URL standardization to dramatically improve scanning efficiency

- **多格式导出**：支持 Excel 和 JSON 格式的结果导出，便于后续分析  
  **Multi-format Export**: Export results in both Excel (.xlsx) and JSON formats for seamless analysis

- **重点资产提取**：自动识别并导出关键系统资产，突出显示高价值目标  
  **Key Asset Extraction**: Automatically identifies and exports critical systems, highlighting high-value targets

- **线程控制**：可自定义并发线程数，灵活调整扫描速度  
  **Thread Control**: Customize concurrency level with `-T` flag to balance speed and stability

- **误报修复**：优化算法，减少 GeoServer 等常见误报问题  
  **False Positive Reduction**: Fixed common false positives (e.g., GeoServer) with refined signature matching

- **3万+精准指纹库**：内置超过 30,000 条经过验证的主动指纹规则，覆盖主流框架、中间件、API 和漏洞特征  
  **30,000+ Precision Fingerprints**: Built-in library of over 30,000 validated active fingerprint rules covering mainstream frameworks, middleware, APIs, and vulnerability signatures

- **双模式输出**：Excel 文件自动分为“被动指纹”与“主动指纹”两个工作表，结构清晰，便于审计  
  **Dual-mode Output**: Excel files automatically split into two sheets — “Passive Fingerprinting” and “Active Fingerprinting” — for clear audit trails

---

## 🚀 安装

### 从源码编译

```bash
git clone https://github.com/yourusername/muki.git
cd muki
go build -o muki
```

### 设置 Go 代理（推荐，加速依赖下载）

```bash
go env -w GOPROXY=https://goproxy.cn,direct
go mod tidy
go build -o muki
```

### 从 Release 下载（推荐生产环境使用）

访问 [Releases](https://github.com/yourusername/muki/releases) 页面下载预编译的二进制文件（支持 Linux / macOS / Windows）。

---

## 📖 使用方法

### 基本用法

```bash
# 识别单个目标
./muki finger -u http://example.com

# 从文件批量识别（支持 IP 或域名）
./muki finger -l targets.txt

# 指定输出格式和文件（不加-F默认是.xlsx格式）
./muki finger -l targets.txt -o result.xlsx -F xlsx

# 自定义线程数（建议 30~100，视网络环境调整）
./muki finger -l targets.txt -T 50

# 使用代理池（每行一个代理，支持 http/https/socks5）
./muki finger -l targets.txt -P proxies.txt -T 40
```
### 使用事例：
./mukip finger -l ip-port.txt -o ip-fingeresult.xlsx -T 100
### 高级用法

```bash
# 导出为 JSON 格式
./muki finger -u http://example.com -F json -o result.json

---

## 📌 参数说明

```
Usage:
  Muki [command]

Available Commands:
  finger      指纹识别模块
  help        帮助信息

Flags:
      --config string       配置文件路径 (默认是 $HOME/.muki.yaml)
  -F, --format string       输出格式，支持 xlsx 和 json (默认 "xlsx")
  -h, --help                帮助信息
  -l, --local string        从本地文件读取资产进行指纹识别
  -o, --output string       输出结果文件，支持 .json 和 .xlsx 格式
  -P, --proxy-pool string   从文件加载代理池，每行一个代理地址
  -T, --thread int          设置扫描线程数，默认为 20 (default 20)
  -u, --url string          识别单个目标
```

> 💡 **提示**：输出的 `.xlsx` 文件中，`被动指纹` 表记录基于响应头/状态码的初步识别；`主动指纹` 表记录通过精确请求、特征匹配、内容比对得出的高置信度结果。

---

## 🎯 应用场景

- **红队作战**：在信息收集阶段快速识别目标资产，缩小攻击面  
- **渗透测试**：辅助发现 Web 服务、管理后台、API 接口、未授权系统等高价值目标  
- **资产测绘**：对组织内部或客户网络进行自动化指纹测绘与分类  
- **威胁狩猎**：结合其他工具（如 masscan、nmap）构建完整攻击链路  
- **安全评估**：自动化评估目标系统暴露的中间件与框架风险

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来帮助改进 MUKI！

- 报告误报或漏报指纹
- 提交新的指纹规则（JSON 格式）
- 优化 UI 或性能
- 添加对新协议或框架的支持

---

## 📄 许可证

本项目采用 MIT 许可证 — 查看 [LICENSE](LICENSE) 文件了解详情。

---

## 🙏 致谢

- 感谢所有为 Muki 贡献代码、指纹与反馈的开发者  
- 感谢开源社区提供的优秀库：`excelize`, `cobra`, `viper`, `goquery`, `color`  
- 感谢红队社区持续推动工具的创新与实战价值

---

**Developer**: KUKI  
**Language**: Go  
**Version**: v1.0.0+  
**Build Time**: 2025-11-13

> ⚠️ **免责声明**：本工具仅用于合法的安全测试、红队演练与授权资产研究。请严格遵守当地法律法规及道德准则，禁止用于任何非法用途。

---

✅ **已适配 macOS / Linux / Windows**  
✅ **无依赖运行（静态编译）**  
✅ **支持中文路径与 UTF-8 编码**  
✅ **SSL 证书问题已内置修复**

---

如需获取最新指纹库、配置模板或使用教程，请访问项目 Wiki 或提交 Issue。  
Let’s make reconnaissance faster. Let’s make red teaming smarter.
