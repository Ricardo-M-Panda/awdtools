# AWD-Kit 已装 Python 包清单

> 运行时：`D:\AWD-Kit\00-runtime\python\python.exe`（Python 3.12.16 便携版）
> 生成时间：2026-11-17 13:02　共 **266** 个包
> 数据来源：`python -m pip list --format=json`，非手工整理

★ = AWD/CTF 每天会用到的核心包

---

## 一、按用途分类

### Web / 漏洞利用

| 包 | 版本 | 用途 |
|---|---|---|
| ★ `requests` | 2.34.2 | HTTP 请求，打点、复现漏洞、写 exp 的地基 |
| ★ `httpx` | 0.28.1 | 异步 HTTP 客户端，批量探测/并发发包 |
| ★ `beautifulsoup4` | 4.15.0 | HTML 解析，抓表单/链接/隐藏字段 |
| ★ `lxml` | 6.1.3 | XPath + 高性能解析，比 bs4 快 |
| `pyquery` | 2.1.0 | jQuery 风格选择器，写爬虫/解析顺手 |
| `cssselect` | 1.6.0 | CSS 选择器引擎（lxml/pyquery 依赖） |
| ★ `websocket-client` | 1.9.2 | WebSocket 客户端，打实时接口 |
| `websockets` | 17.4 | 异步 WebSocket 库 |
| ★ `jsbeautifier` | 2.0.3 | JS 反混淆/格式化，看前端加密逻辑 |
| ★ `arjun` | 2.2.7 | HTTP 参数发现，找隐藏参数 |
| ★ `wafw00f` | 2.4.2 | WAF 识别，判断目标有没有防护 |
| ★ `PyJWT` | 2.15.1 | JWT 解析/伪造，越权与密钥爆破 |
| `passlib` | 1.7.4 | 口令哈希框架 |
| `bcrypt` | 5.0.0 | bcrypt 哈希/校验 |
| `argon2-cffi` | 25.1.0 | Argon2 哈希 |
| ★ `python-multipart` | 0.0.34 | multipart 表单解析，构造文件上传包 |
| ★ `Flask` | 3.1.3 | 本地起测试服务/写 poc 服务端 |
| `Werkzeug` | 3.1.9 | Flask 底层 WSGI 工具 |
| ★ `Jinja2` | 3.1.6 | 模板引擎，SSTI 练习与利用 |
| ★ `SQLAlchemy` | 2.1.8 | ORM，读源码时看查询逻辑 |
| ★ `PySocks` | 1.7.1 | SOCKS 代理，配合隧道打内网 |
| `requests-toolbelt` | 1.0.0 | 流式上传/多段编码 |
| `urllib3` | 2.8.0 | requests 底层连接池 |
| `certifi` | 2026.10.23 | CA 证书包 |
| `chardet` | 7.7.0 | 编码探测 |
| `charset-normalizer` | 3.5.2 | 编码探测（requests 新版依赖） |
| `idna` | 3.20 | 国际化域名 |
| `h11` | 0.16.0 | HTTP/1.1 状态机 |
| `h2` | 4.4.1 | HTTP/2 协议实现 |
| `hpack` | 4.2.0 | HTTP/2 头部压缩 |
| `hyperframe` | 6.1.0 | HTTP/2 帧 |
| `wsproto` | 1.3.2 | WebSocket 协议 |
| `starlette` | 1.10.0 | ASGI 框架 |
| `uvicorn` | 0.54.0 | ASGI 服务器 |
| `sse-starlette` | 3.7.0 | SSE 支持 |

### 流量 / 网络 / 内网

| 包 | 版本 | 用途 |
|---|---|---|
| ★ `scapy` | 2.8.0 | 构造/解析任意协议包，发包与嗅探 |
| ★ `dpkt` | 1.9.8 | 轻量 pcap 解析，比 scapy 快 |
| ★ `pyshark` | 0.6 | tshark 的 Python 封装，深度解析 pcap |
| `pyshark-mcp` | 0.2.2 | 上面那个的 MCP 服务端 |
| ★ `mitmproxy` | 12.3.1 | 中间人代理，改包/重放/看 HTTPS（装证书后） |
| `mitmproxy_rs` | 0.12.16 | mitmproxy 的 Rust 内核 |
| ★ `impacket` | 0.13.1 | SMB/WMI/LDAP 等协议栈，Windows 横向 |
| ★ `ldap3` | 2.9.1 | LDAP 查询，AD 信息收集 |
| `ldapdomaindump` | 0.10.0 | AD 域信息批量导出 |
| ★ `dnspython` | 2.9.2 | DNS 查询，dnslog/盲打 |
| ★ `netaddr` | 1.3.0 | IP/CIDR 计算 |
| ★ `mmh3` | 5.3.1 | MurmurHash3，算 favicon hash 做指纹 |
| `xxhash` | 4.1.0 | xxHash，快速哈希/目录扫描去重 |
| `pydivert` | 3.1.3 | Windows 抓包/改包驱动（WinDivert） |
| `pyserial` | 3.5 | 串口通信，硬件/工控方向 |
| `aioquic` | 1.2.0 | QUIC / HTTP/3 |
| `pylsqpack` | 0.3.24 | QPACK（HTTP/3 头部压缩） |
| `kaitaistruct` | 0.11 | 二进制协议结构化解析 |
| ★ `construct` | 2.10.70 | 二进制结构定义与解析 |
| `aiofile` | 3.12.3 | 异步文件 IO |
| `caio` | 0.12.10 | 异步 IO 底层 |

### 二进制 / PWN / 逆向

| 包 | 版本 | 用途 |
|---|---|---|
| ★ `pwntools` | 4.15.0 | EXP 编写框架：交互、打包、ELF、shellcraft |
| ★ `capstone` | 5.0.9 | 反汇编引擎 |
| ★ `keystone-engine` | 0.9.2 | 汇编引擎（写 shellcode） |
| ★ `unicorn` | 2.1.2 | CPU 模拟器，跑单段代码 |
| ★ `z3-solver` | 5.3.3.0 | 约束求解，逆向/CTF 神器 |
| ★ `sympy` | 1.14.0 | 符号计算，密码学题 |
| ★ `angr` | 10.0.7 | 符号执行框架，自动找路径 |
| `angr-data` | 0.2.0 | angr 的数据包 |
| `archinfo` | 10.0.7 | angr 架构信息 |
| `cle` | 10.0.7 | angr 的 ELF/PE 加载器 |
| `pyvex` | 10.0.7 | VEX IR |
| ★ `pypcode` | 4.0.1 | Ghidra 反编译器的 Python 绑定 |
| ★ `ropper` | 1.13.13 | ROP gadget 搜索 |
| ★ `ROPGadget` | 7.7 | ROP gadget 搜索（另一个实现） |
| ★ `pyelftools` | 0.33 | ELF 解析，读节表/符号 |
| ★ `pefile` | 2024.8.26 | PE 解析，Windows 样本分析 |
| ★ `lief` | 1.0.0 | ELF/PE/Mach-O 修改，打补丁/改入口 |
| ★ `frida` | 17.26.3 | 动态插桩，Hook/脱壳 |
| ★ `frida-tools` | 14.13.1 | frida 命令行工具集 |
| `frida-mcp-server` | 1.0.1 | frida 的 MCP 服务端 |
| `ghidra-mcp` | 2.0.0 | Ghidra 的 MCP 桥 |
| `minidump` | 0.0.24 | Windows minidump 解析 |
| `uefi_firmware` | 1.17 | UEFI 固件解析 |
| `unix-ar` | 0.2.1 | ar 归档解析 |
| `arpy` | 1.1.1 | ar 归档解析（另一实现） |
| `pyxbe` | 1.0.4 | Xbox XBE 格式 |
| `pyxdia` | 0.1.1 | PDB/调试符号 |
| ★ `pydemumble` | 0.1.3 | C++ 符号反修饰 |
| `filebytes` | 0.10.2 | 文件字节流封装 |
| `cxxheaderparser` | 2.2.0 | C++ 头文件解析 |
| `intervaltree` | 3.2.1 | 区间树（angr 依赖） |
| `networkx` | 3.7 | 图算法（angr 依赖） |
| `mulpyplexer` | 0.9 | 并行 map（angr 依赖） |
| ★ `pywin32` | 311 | Windows API 调用 |
| `pywin32-ctypes` | 0.2.3 | 轻量 Windows API |

### 密码学

| 包 | 版本 | 用途 |
|---|---|---|
| ★ `pycryptodome` | 4.5.0 | AES/RSA/哈希等一站式实现 |
| ★ `pycryptodomex` | 3.24.2 | 同上的独立命名空间版本 |
| ★ `cryptography` | 50.0.2 | 现代密码学库（TLS/X509） |
| ★ `gmpy2` | 2.3.2 | 大整数运算，RSA 题必备 |
| `mpmath` | 1.3.0 | 任意精度浮点 |
| `PyNaCl` | 1.6.2 | libsodium 绑定（Ed25519/curve25519） |
| `joserfc` | 1.8.0 | JOSE/JWT 底层 |
| `Authlib` | 1.9.8 | OAuth/JOSE 全家桶 |
| `pyasn1` | 0.6.5 | ASN.1 编解码 |
| `pyasn1_modules` | 0.4.2 | ASN.1 常用模块 |
| `pyOpenSSL` | 26.4.0 | OpenSSL 绑定 |
| `cffi` | 2.1.1 | C 扩展调用（cryptography 依赖） |
| `pycparser` | 3.11 | C 解析器 |

### 取证 / 文档 / 杂项解析

| 包 | 版本 | 用途 |
|---|---|---|
| ★ `volatility3` | 2.28.2 | 内存取证框架，抓密码/进程/网络 |
| ★ `oletools` | 0.60.2 | Office 宏分析（olevba/mraptor） |
| `olefile` | 0.47 | OLE 复合文档解析 |
| `pcodedmp` | 1.2.6 | VBA 伪代码反编译 |
| ★ `msoffcrypto-tool` | 6.1.0 | 加密 Office 文档解密 |
| ★ `regipy` | 6.5.0 | Windows 注册表解析 |
| ★ `yara-python` | 4.5.4 | YARA 规则匹配，扫样本/扫马 |
| `defusedxml` | 0.7.1 | 安全 XML 解析（防 XXE） |
| `dicttoxml` | 1.7.16 | dict 转 XML（构造 XXE payload） |
| `pyperclip` | 1.11.0 | 剪贴板 |

### 数据库 / 缓存

| 包 | 版本 | 用途 |
|---|---|---|
| ★ `PyMySQL` | 1.2.4 | MySQL 客户端，直连改库/读数据 |
| ★ `psycopg2-binary` | 2.9.13 | PostgreSQL 客户端 |
| ★ `pymongo` | 4.20.0 | MongoDB 客户端（未授权访问常见） |
| ★ `redis` | 8.1.0 | Redis 客户端（未授权/写马） |
| `peewee` | 3.19.0 | 轻量 ORM |
| `fakeredis` | 2.34.1 | Redis 模拟器（本地测试） |
| `burner-redis` | 0.1.7 | Redis 工具 |
| `lmdb` | 3.0.0 | LMDB 数据库 |
| `diskcache` | 5.6.3 | 磁盘缓存 |

### LLM / MCP / 脚本工具链

| 包 | 版本 | 用途 |
|---|---|---|
| ★ `mcp` | 1.12.2 | MCP Python SDK（写 MCP server 用） |
| `mcp-types` | 2.3.0 | MCP 类型定义 |
| ★ `fastmcp` | 2.14.7 | 高层 MCP 框架 |
| `pydantic` | 2.11.10 | 数据校验（MCP 工具签名） |
| `pydantic-settings` | 2.16.3 | 配置管理 |
| ★ `semgrep` | 1.135.0 | 源码静态审计，找 SQLi/RCE |
| `semgrep-mcp` | 0.9.0 | semgrep 的 MCP（已废弃，仅留备份） |
| ★ `PyYAML` | 6.0.3 | YAML 读写 |
| `ruamel.yaml` | 0.19.1 | 保留注释的 YAML |
| `tomli` | 2.0.2 | TOML 解析 |
| `python-dotenv` | 1.2.4 | .env 读取 |
| `jsonschema` | 4.25.1 | JSON Schema 校验 |
| `jsonref` | 1.1.0 | JSON $ref 解析 |
| `typer` | 0.29.1 | 命令行框架 |
| `click` | 8.1.8 | 命令行框架 |
| ★ `rich` | 15.0.0 | 终端富文本/表格 |
| `Pygments` | 2.21.0 | 语法高亮 |
| ★ `tabulate` | 0.10.0 | 表格输出 |
| ★ `tqdm` | 4.70.1 | 进度条 |
| ★ `colorama` | 0.4.6 | Windows 彩色输出 |
| `termcolor` | 3.3.0 | 彩色输出 |
| `colorclass` | 2.2.2 | 彩色输出 |
| `pyfiglet` | 1.0.4 | ASCII 大字 |
| `shellingham` | 1.5.4 | shell 探测 |
| `prompt_toolkit` | 3.0.53 | 交互式命令行 |
| `urwid` | 4.0.13 | TUI 框架 |
| `invoke` | 3.0.3 | 任务执行 |
| `plumbum` | 2.0.2 | shell 组合 |
| ★ `watchfiles` | 1.3.0 | 文件变化监听 |
| ★ `psutil` | 7.2.2 | 进程/系统信息，查马找异常进程 |
| `python-dateutil` | 4.0.0 | 日期解析 |
| `pytz` | 2026.6 | 时区 |
| `tzdata` | 2026.6 | 时区数据 |
| `packaging` | 26.3 | 版本比较 |
| `setuptools` | 80.10.2 | 打包工具（锁 <81 保 pkg_resources） |
| `pip` | 26.3 | 包管理 |
| `win_unicode_console` | 0.5 | Windows 控制台编码 |
| `pyreadline3` | 3.5.6 | Windows readline |
| `easygui` | 0.98.3 | 简易 GUI 弹窗 |
| `protobuf` | 7.36.2 | Protocol Buffers |
| `zstandard` | 0.25.0 | zstd 压缩 |
| `backports.zstd` | 1.7.0 | zstd 兼容层 |
| `brotli` | 1.2.1 | brotli 压缩（HTTP 解压） |
| `bitarray` | 3.12.4 | 位数组 |
| `bitstring` | 4.4.0 | 位串 |
| `boltons` | 21.0.0 | 通用工具集 |
| `glom` | 22.1.0 | 嵌套数据取值 |
| `beartype` | 0.23.1 | 运行时类型检查 |
| `uncalled-for` | 0.6.1 | 空值处理 |
| `wrapt` | 1.17.3 | 装饰器工具 |

---

## 二、完整清单（按字母序）

共 266 个。标 ★ 的是上面分类里提到的核心包。

| # | 包 | 版本 |
|---|---|---|
| 1 | `aiofile` | 3.12.3 |
| 2 | `aioquic` | 1.2.0 |
| 3 | ★ `angr` | 10.0.7 |
| 4 | `angr-data` | 0.2.0 |
| 5 | `annotated-doc` | 0.0.6 |
| 6 | `annotated-types` | 0.8.0 |
| 7 | `anyio` | 4.16.0 |
| 8 | `appdirs` | 1.4.4 |
| 9 | `archinfo` | 10.0.7 |
| 10 | `argon2-cffi` | 25.1.0 |
| 11 | `argon2-cffi-bindings` | 26.2.0 |
| 12 | ★ `arjun` | 2.2.7 |
| 13 | `arpy` | 1.1.1 |
| 14 | `asgiref` | 3.12.1 |
| 15 | `attrs` | 26.1.0 |
| 16 | `Authlib` | 1.9.8 |
| 17 | `backports.zstd` | 1.7.0 |
| 18 | `bcrypt` | 5.0.0 |
| 19 | `beartype` | 0.23.1 |
| 20 | ★ `beautifulsoup4` | 4.15.0 |
| 21 | `bitarray` | 3.12.4 |
| 22 | `bitstring` | 4.4.0 |
| 23 | `blinker` | 1.9.0 |
| 24 | `boltons` | 21.0.0 |
| 25 | `bracex` | 3.2.3 |
| 26 | `brotli` | 1.2.1 |
| 27 | `burner-redis` | 0.1.7 |
| 28 | `cachetools` | 7.3.2 |
| 29 | `caio` | 0.12.10 |
| 30 | ★ `capstone` | 5.0.9 |
| 31 | `cart` | 1.2.3 |
| 32 | `certifi` | 2026.10.23 |
| 33 | `cffi` | 2.1.1 |
| 34 | `chardet` | 7.7.0 |
| 35 | `charset-normalizer` | 3.5.2 |
| 36 | `cle` | 10.0.7 |
| 37 | `click` | 8.1.8 |
| 38 | `click-option-group` | 0.5.10 |
| 39 | `cloudpickle` | 3.1.2 |
| 40 | ★ `colorama` | 0.4.6 |
| 41 | `colorclass` | 2.2.2 |
| 42 | `colored-traceback` | 0.4.2 |
| 43 | ★ `construct` | 2.10.70 |
| 44 | `cronsim` | 2.8 |
| 45 | ★ `cryptography` | 50.0.2 |
| 46 | `cssselect` | 1.6.0 |
| 47 | `cxxheaderparser` | 2.2.0 |
| 48 | `cyclopts` | 5.5.1 |
| 49 | `defusedxml` | 0.7.1 |
| 50 | `Deprecated` | 3.0.1 |
| 51 | `dicttoxml` | 1.7.16 |
| 52 | `diskcache` | 5.6.3 |
| 53 | ★ `dnspython` | 2.9.2 |
| 54 | `docstring_parser` | 0.18.0 |
| 55 | ★ `dpkt` | 1.9.8 |
| 56 | `easygui` | 0.98.3 |
| 57 | `EditorConfig` | 0.17.1 |
| 58 | `email-validator` | 2.4.0 |
| 59 | `exceptiongroup` | 1.2.2 |
| 60 | `face` | 26.0.1 |
| 61 | `fakeredis` | 2.34.1 |
| 62 | ★ `fastmcp` | 2.14.7 |
| 63 | `fastmcp-slim` | 4.2.0 |
| 64 | `filebytes` | 0.10.2 |
| 65 | ★ `Flask` | 3.1.3 |
| 66 | ★ `frida` | 17.26.3 |
| 67 | `frida-mcp-server` | 1.0.1 |
| 68 | ★ `frida-tools` | 14.13.1 |
| 69 | `ghidra-mcp` | 2.0.0 |
| 70 | `gitdb` | 4.0.12 |
| 71 | `GitPython` | 3.2.1 |
| 72 | `glom` | 22.1.0 |
| 73 | ★ `gmpy2` | 2.3.2 |
| 74 | `googleapis-common-protos` | 1.75.0 |
| 75 | `griffelib` | 2.4.1 |
| 76 | `h11` | 0.16.0 |
| 77 | `h2` | 4.4.1 |
| 78 | `hpack` | 4.2.0 |
| 79 | `httpcore` | 1.0.9 |
| 80 | `httpcore2` | 2.16.2 |
| 81 | ★ `httpx` | 0.28.1 |
| 82 | `httpx-sse` | 0.4.3 |
| 83 | `httpx2` | 2.16.2 |
| 84 | `hyperframe` | 6.1.0 |
| 85 | `idna` | 3.20 |
| 86 | ★ `impacket` | 0.13.1 |
| 87 | `importlib_metadata` | 7.1.0 |
| 88 | `inflection` | 0.5.1 |
| 89 | `intervaltree` | 3.2.1 |
| 90 | `invoke` | 3.0.3 |
| 91 | `itsdangerous` | 2.2.0 |
| 92 | `jaraco.classes` | 3.4.0 |
| 93 | `jaraco.context` | 6.1.2 |
| 94 | `jaraco.functools` | 4.6.0 |
| 95 | ★ `Jinja2` | 3.1.6 |
| 96 | `joserfc` | 1.8.0 |
| 97 | ★ `jsbeautifier` | 2.0.3 |
| 98 | `jsonref` | 1.1.0 |
| 99 | `jsonschema` | 4.25.1 |
| 100 | `jsonschema-path` | 0.5.0 |
| 101 | `jsonschema-specifications` | 2025.9.1 |
| 102 | `kaitaistruct` | 0.11 |
| 103 | `keyring` | 25.7.0 |
| 104 | ★ `keystone-engine` | 0.9.2 |
| 105 | ★ `ldap3` | 2.9.1 |
| 106 | `ldapdomaindump` | 0.10.0 |
| 107 | ★ `lief` | 1.0.0 |
| 108 | `lmdb` | 3.0.0 |
| 109 | `lupa` | 2.8 |
| 110 | ★ `lxml` | 6.1.3 |
| 111 | `Mako` | 1.4.3 |
| 112 | `markdown-it-py` | 4.3.0 |
| 113 | `MarkupSafe` | 3.0.4 |
| 114 | ★ `mcp` | 1.12.2 |
| 115 | `mcp-types` | 2.3.0 |
| 116 | `mdurl` | 0.1.2 |
| 117 | `minidump` | 0.0.24 |
| 118 | ★ `mitmproxy` | 12.3.1 |
| 119 | `mitmproxy-windows` | 0.12.16 |
| 120 | `mitmproxy_rs` | 0.12.16 |
| 121 | ★ `mmh3` | 5.3.1 |
| 122 | `more-itertools` | 11.2.1 |
| 123 | `mpmath` | 1.3.0 |
| 124 | `msgspec` | 0.22.0 |
| 125 | ★ `msoffcrypto-tool` | 6.1.0 |
| 126 | `mulpyplexer` | 0.9 |
| 127 | ★ `netaddr` | 1.3.0 |
| 128 | `networkx` | 3.7 |
| 129 | `olefile` | 0.47 |
| 130 | ★ `oletools` | 0.60.2 |
| 131 | `openapi-pydantic` | 0.6.0 |
| 132 | `opentelemetry-api` | 1.25.0 |
| 133 | `opentelemetry-exporter-otlp-proto-common` | 1.25.0 |
| 134 | `opentelemetry-exporter-otlp-proto-http` | 1.25.0 |
| 135 | `opentelemetry-instrumentation` | 0.46b0 |
| 136 | `opentelemetry-instrumentation-requests` | 0.46b0 |
| 137 | `opentelemetry-instrumentation-threading` | 0.58b0 |
| 138 | `opentelemetry-proto` | 1.25.0 |
| 139 | `opentelemetry-sdk` | 1.25.0 |
| 140 | `opentelemetry-semantic-conventions` | 0.46b0 |
| 141 | `opentelemetry-util-http` | 0.46b0 |
| 142 | `packaging` | 26.3 |
| 143 | `paramiko` | 5.1.0 |
| 144 | `passlib` | 1.7.4 |
| 145 | `pathable` | 0.6.0 |
| 146 | `pathvalidate` | 3.3.1 |
| 147 | `pcodedmp` | 1.2.6 |
| 148 | `peewee` | 3.19.0 |
| 149 | ★ `pefile` | 2024.8.26 |
| 150 | `phpserialize` | 1.3 |
| 151 | `pip` | 26.3 |
| 152 | `platformdirs` | 4.14.5 |
| 153 | `plumbum` | 2.0.2 |
| 154 | `prometheus_client` | 0.26.0 |
| 155 | `prompt_toolkit` | 3.0.53 |
| 156 | `protobuf` | 7.36.2 |
| 157 | ★ `psutil` | 7.2.2 |
| 158 | ★ `psycopg2-binary` | 2.9.13 |
| 159 | `publicsuffix2` | 2.20191221 |
| 160 | ★ `pwntools` | 4.15.0 |
| 161 | `py-key-value-aio` | 0.3.0 |
| 162 | `py-key-value-shared` | 0.3.0 |
| 163 | `pyasn1` | 0.6.5 |
| 164 | `pyasn1_modules` | 0.4.2 |
| 165 | `pycparser` | 3.11 |
| 166 | ★ `pycryptodome` | 4.5.0 |
| 167 | ★ `pycryptodomex` | 3.24.2 |
| 168 | `pydantic` | 2.11.10 |
| 169 | `pydantic-settings` | 2.16.3 |
| 170 | `pydantic_core` | 2.33.2 |
| 171 | ★ `pydemumble` | 0.1.3 |
| 172 | `pydivert` | 3.1.3 |
| 173 | `pydocket` | 0.28.0 |
| 174 | ★ `pyelftools` | 0.33 |
| 175 | `pyfiglet` | 1.0.4 |
| 176 | `Pygments` | 2.21.0 |
| 177 | ★ `PyJWT` | 2.15.1 |
| 178 | `pylsqpack` | 0.3.24 |
| 179 | ★ `pymongo` | 4.20.0 |
| 180 | ★ `PyMySQL` | 1.2.4 |
| 181 | `PyNaCl` | 1.6.2 |
| 182 | `pyOpenSSL` | 26.4.0 |
| 183 | `pyparsing` | 3.3.3 |
| 184 | ★ `pypcode` | 4.0.1 |
| 185 | `pyperclip` | 1.11.0 |
| 186 | `pyquery` | 2.1.0 |
| 187 | `pyreadline3` | 3.5.6 |
| 188 | `pyserial` | 3.5 |
| 189 | ★ `pyshark` | 0.6 |
| 190 | `pyshark-mcp` | 0.2.2 |
| 191 | ★ `PySocks` | 1.7.1 |
| 192 | `python-dateutil` | 4.0.0 |
| 193 | `python-dotenv` | 1.2.4 |
| 194 | `python-json-logger` | 4.2.0 |
| 195 | ★ `python-multipart` | 0.0.34 |
| 196 | `pytz` | 2026.6 |
| 197 | `pyvex` | 10.0.7 |
| 198 | ★ `pywin32` | 311 |
| 199 | `pywin32-ctypes` | 0.2.3 |
| 200 | `pyxbe` | 1.0.4 |
| 201 | `pyxdia` | 0.1.1 |
| 202 | ★ `PyYAML` | 6.0.3 |
| 203 | `ratelimit` | 2.2.1 |
| 204 | ★ `redis` | 8.1.0 |
| 205 | `referencing` | 0.37.0 |
| 206 | ★ `regipy` | 6.5.0 |
| 207 | ★ `requests` | 2.34.2 |
| 208 | `requests-toolbelt` | 1.0.0 |
| 209 | ★ `rich` | 15.0.0 |
| 210 | `rich-rst` | 2.2.0 |
| 211 | ★ `ROPGadget` | 7.7 |
| 212 | ★ `ropper` | 1.13.13 |
| 213 | `rpds-py` | 2026.9.1 |
| 214 | `rpyc` | 6.0.2 |
| 215 | `ruamel.yaml` | 0.19.1 |
| 216 | `ruamel.yaml.clib` | 0.2.15 |
| 217 | ★ `scapy` | 2.8.0 |
| 218 | `semantic-version` | 2.10.0 |
| 219 | ★ `semgrep` | 1.135.0 |
| 220 | `semgrep-mcp` | 0.9.0 |
| 221 | `service-identity` | 26.1.0 |
| 222 | `setuptools` | 80.10.2 |
| 223 | `shellingham` | 1.5.4 |
| 224 | `six` | 1.17.0 |
| 225 | `smmap` | 5.0.3 |
| 226 | `sortedcontainers` | 2.4.0 |
| 227 | `soupsieve` | 4.1.1 |
| 228 | ★ `SQLAlchemy` | 2.1.8 |
| 229 | `sse-starlette` | 3.7.0 |
| 230 | `starlette` | 1.10.0 |
| 231 | `structlog` | 26.1.0 |
| 232 | ★ `sympy` | 1.14.0 |
| 233 | ★ `tabulate` | 0.10.0 |
| 234 | `termcolor` | 3.3.0 |
| 235 | `tibs` | 0.5.7 |
| 236 | `tomli` | 2.0.2 |
| 237 | `tornado` | 6.5.10 |
| 238 | ★ `tqdm` | 4.70.1 |
| 239 | `truststore` | 0.10.5 |
| 240 | `typer` | 0.29.1 |
| 241 | `typing-inspection` | 0.4.5 |
| 242 | `typing_extensions` | 4.16.0 |
| 243 | `tzdata` | 2026.6 |
| 244 | `uefi_firmware` | 1.17 |
| 245 | `uncalled-for` | 0.6.1 |
| 246 | ★ `unicorn` | 2.1.2 |
| 247 | `unix-ar` | 0.2.1 |
| 248 | `urllib3` | 2.8.0 |
| 249 | `urwid` | 4.0.13 |
| 250 | `uvicorn` | 0.54.0 |
| 251 | ★ `volatility3` | 2.28.2 |
| 252 | ★ `wafw00f` | 2.4.2 |
| 253 | ★ `watchfiles` | 1.3.0 |
| 254 | `wcmatch` | 8.5.2 |
| 255 | `wcwidth` | 0.9.4 |
| 256 | ★ `websocket-client` | 1.9.2 |
| 257 | `websockets` | 17.4 |
| 258 | `Werkzeug` | 3.1.9 |
| 259 | `win_unicode_console` | 0.5 |
| 260 | `wrapt` | 1.17.3 |
| 261 | `wsproto` | 1.3.2 |
| 262 | `xxhash` | 4.1.0 |
| 263 | ★ `yara-python` | 4.5.4 |
| 264 | ★ `z3-solver` | 5.3.3.0 |
| 265 | `zipp` | 4.1.2 |
| 266 | `zstandard` | 0.25.0 |

---

## 三、常用一行命令

```powershell
$PY = 'D:\AWD-Kit\00-runtime\python\python.exe'

# 查包
& $PY -m pip list
& $PY -m pip show pwntools

# 装包（走代理）
$env:HTTPS_PROXY='http://127.0.0.1:7897'
& $PY -m pip install requests

# 常用导入自检
& $PY -c "import pwn,requests,scapy,angr,z3;print('ok')"
```

### 版本锁定注意

这台机器上有几组互相牵制的版本，**升级前先看一眼**：

| 包 | 锁定版本 | 原因 |
|---|---|---|
| `mcp` | 实际 `1.12.2` | 升到 1.30+ 会与 semgrep 声明的 `mcp==1.29.0` 冲突；1.12.2 实测 ghidra-mcp / awd-llm / frida 全部可用，暂不动 |
| `pydantic` | `2.11.10` | 2.12+ 删了 `eval_type_backport`，mcp 的 FastMCP 会 import 失败 |
| `setuptools` | `<81` | 81+ 移除 `pkg_resources`，semgrep/opentelemetry 依赖它 |
| `protobuf` | `>=5.28` | 4.x 缺 `runtime_version`，angr/pwntools 起不来 |
