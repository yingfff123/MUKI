<p>
    <strong>一款指纹识别工具</strong>
</p>

<p align="center">
    <a href="https://github.com/yourusername/muki/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg"></a>
    <a href="https://github.com/yourusername/muki/releases"><img src="https://img.shields.io/github/v/release/yourusername/muki"></a>
    <a href="https://golang.org/"><img src="https://img.shields.io/badge/language-Go-blue.svg"></a>
</p>
</p>
<p align="center">
  <img width="324" height="120" alt="Muki - Active Asset Fingerprinting Tool" src="https://github.com/user-attachments/assets/fd331a9e-7628-462e-9189-3eb8387323c6" />
</p>
<p align="center">
Muki 是一款专为红队作战设计的主动资产指纹识别工具。在信息收集阶段，Muki 能够帮助安全研究人员快速从 C 段、大量杂乱的资产中精准定位到易被攻击的系统，从而实施进一步的渗透测试。

Muki is a brand-new active asset fingerprinting tool designed for red team operations. During reconnaissance, Muki enables security researchers to rapidly pinpoint vulnerable systems from chaotic C-class segments and massive asset lists, enabling targeted exploitation.

---
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
![gif1114](https://github.com/user-attachments/assets/9e43cbb9-360d-4c4e-976a-ecab130dcc3f)


安装

直接拉取linux版本

```bash
git clone https://github.com/yourusername/muki.git 
cd muki|chmod +x muki-linux-amd64
./muki-linux-amd64

从 Release 下载（推荐生产环境使用）

访问 [Releases](https://github.com/yingfff123/MUKI/releases) 页面下载预编译的二进制文件（支持 Linux / macOS / Windows）。

---
使用方法
基本用法

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
使用事例：
./mukip finger -l ip-port.txt -o ip-fingeresult.xlsx -T 100
高级用法
导出为 JSON 格式
./muki finger -u http://example.com -F json -o result.json

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


---

