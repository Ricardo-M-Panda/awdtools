# AWD-Kit —— AWD 攻防比赛工具箱

> 位置：**本文件所在目录**（当前实测位置：`D:\AWD-Kit\`）（本文档里的 `AWD-Kit` 均指这个根目录，整个文件夹可随意移动/改名）
> 体积：完整约 **8.6 GB**（含 3.2 GB 原始安装包 `_archives\`，可删；删后约 5.4 GB）
> 平台：Windows 10/11 x64 / 全部为**便携版**，不写注册表、不污染系统 PATH

---

## 零、换机器 / 发给别人时

1. 整个目录拷过去即可，**不需要安装**。
2. 首次运行先做一次自检：双击 `首次运行.cmd`（或 `powershell -File verify.ps1`）。
3. 如果要挂 MCP：`powershell -ExecutionPolicy Bypass -File mcp\install-mcp.ps1`（路径自动识别）。
4. 如果要把 skill 也装过去：把 `skills\awd-competition` 拷到 `%USERPROFILE%\.dsh\skills\`。
5. 打包发送用 `make-portable-zip.ps1`（默认剔除 `_archives`，避免 8.6G）。
6. **唯一会因为「换目录」失效的东西**：pip 生成的命令行入口（`pwn`、`ropper`、`vol.py`、`angr` 等 `.exe`）。
   这些 exe 内部写死了 Python 的绝对路径。修法（需联网）：
   ```powershell
   . .\activate.ps1
   python -m pip install --force-reinstall --no-deps pwntools ropper ROPGadget volatility3
   ```
   或者干脆用 `python -m` 方式调用；`awd.py`、`webshell_scan.py`、`sqlmap.py` 都是 `python xxx.py`，不受影响。

---

## 一、3 分钟上手

```powershell
# 1. 激活环境（当前窗口临时生效；先 cd 到你实际放 AWD-Kit 的目录）
cd D:\tools\AWD-Kit
. .\activate.ps1

# 2. 填靶机信息
copy 08-awd\config.example.json 08-awd\config.json
notepad 08-awd\config.json

# 3. 一键：推防守脚本 + 收旗 + 交旗
python 08-awd\awd.py push -l 08-awd\defense.sh -r /tmp/d.sh -C "bash /tmp/d.sh all"
python 08-awd\awd.py submit -c 08-awd\config.json

# 4. 常驻收旗（放后台）
python 08-awd\awd.py loop -c 08-awd\config.json --interval 30
```

`cmd` 用户用 `activate.cmd`。

---

## 二、目录结构

| 目录 | 大小 | 内容 |
|---|---|---|
| `00-runtime\` | 1.4 GB | 便携 Python 3.12.16 / Node 26.13.1 / Go 1.27.4 / JDK 21.0.13 / 7-Zip 25.01 |
| `01-recon\` | 342 MB | nmap 7.993(+ncat)、fscan 2.2.2、kscan、httpx 1.12、nuclei 3.11、linpeas、winPEAS |
| `02-web\` | 186 MB | Burp 2026.11、sqlmap 1.10、ffuf 2.3、dirsearch、xpoc(xray)、CyberChef、字典 |
| `03-binary\` | 2.2 GB | Ghidra 12.2、radare2 6.2.6、rizin 0.9.1、x64dbg、DIE 4.0、hashcat 8.0、Wireshark/tshark 4.6.9 |
| `04-tunnel\` | 88 MB | frp 0.72、chisel 1.12、Neo-reGeorg、Venom、Stowaway(win/linux) |
| `05-webshell\` | 314 MB | 蚁剑 4.0.3、冰蝎 4.1、哥斯拉 4.0.1、Nishang、PowerCat |
| `06-c2\` | 678 MB | Sliver 1.7.9（client/win server/linux server）、Metasploit MSI |
| `07-revshell\` | — | ConPtyShell（`ConPtyShell.exe` / `ConPtyShell_dotnet2.exe`） |
| `08-awd\` | — | 自制实战脚本（见第四节） |
| `mcp\` | 14 MB | `awd-tools` MCP server + DSH 挂载脚本 |
| `skills\` | — | `awd-competition` skill 源文件 |
| `_archives\` | 3.2 GB | 所有原始下载包（校验/重装用，可删） |

---

## 三、工具速查

### 侦察
```powershell
nmap -sV -Pn -T4 --top-ports 1000 10.0.0.0/24
nmap -sV -Pn -p- --min-rate 2000 10.0.0.5
fscan -h 10.0.0.0/24 -p 1-65535
httpx -u http://10.0.0.5 -title -tech-detect -status-code
nuclei -u http://10.0.0.5 -severity critical,high
```

### Web
```powershell
ffuf -u http://T/\FUZZ -w 02-web\wordlist\common.txt -fc 404 -e .php,.bak,.zip
python 02-web\sqlmap\sqlmap.py -u "http://T/?id=1" --batch --dbs
02-web\xpoc.exe scan --target http://T          # xray 新版
02-web\burpsuite_windows-x64_v2026_11.exe       # 需 JDK（activate 后自带）
```

### 二进制 / 逆向
```powershell
03-binary\ghidra\ghidraRun.bat                   # 需 JDK21
r2 -A ./pwn                                     # radare2
03-binary\x64dbg\release\x96dbg.exe              # Windows 调试
03-binary\die\die.exe                            # 查壳
03-binary\hashcat\hashcat.exe -m 0 -a 0 hash.txt wordlist.txt
```

### 隧道 / 代理
```powershell
04-tunnel\frp\frpc.exe -c frpc.ini
04-tunnel\chisel\chisel.exe client -R socks 1080:127.0.0.1:1080 http://VPS:8080
python 04-tunnel\neoreg\neoreg.py -k PASS -u http://target/tunnel.php -p 1080
```

### C2 / 反弹 shell
```powershell
06-c2\sliver-server_windows-amd64.exe
# 控制台内： mtls --lport 8888
#           generate --mtls IP:8888 --os linux --save /tmp/
06-c2\metasploitframework-latest.msi             # 双击安装后可用 msfvenom
```
> 各语言反弹 shell 一行命令、编码绕过、交互式升级：见 **`08-awd\revshell.md`**

### Webshell 管理
```powershell
05-webshell\AntSword\AntSword.exe                 # 蚁剑
05-webshell\Behinder\Behinder.jar                  # 冰蝎（java -jar）
05-webshell\godzilla.jar                           # 哥斯拉（java -jar）
```

---

## 四、AWD 自制脚本（`08-awd\`）

| 文件 | 作用 |
|---|---|
| `awd.py` | 多靶机 **收旗 / 交旗 / 批量执行 / 推送 / 拉取**，支持并发、去重、断点续跑 |
| `defense.sh` | 靶机端防守：`baseline` 基线 / `backup` 备份 / `scan` 查马 / `protect` 护旗 / `watch` 监控 / `restore` 恢复 / `all` 一键 |
| `webshell_scan.py` | 本地扫 webshell，覆盖蚁剑/冰蝎/哥斯拉/一句话，打分排序 |
| `revshell.md` | 反弹 shell 全语言速查 + 绕过 + 升级交互 shell |
| `checklist.md` | AWD 时间线 checklist（赛前/开赛/每轮/防守优先级） |
| `config.example.json` | 靶机 + 交旗接口配置模板 |

常用命令：
```powershell
python 08-awd\awd.py collect -c 08-awd\config.json           # 只看不收
python 08-awd\awd.py submit  -c 08-awd\config.json           # 收 + 交
python 08-awd\awd.py loop    -c 08-awd\config.json --interval 30
python 08-awd\awd.py exec    -c 08-awd\config.json -C "chmod 400 /flag"
python 08-awd\awd.py pull    -c 08-awd\config.json -r /var/www/html -o .\src
```

---

## 五、MCP（已挂载到 DeepSeek Harness）

已注册 **8 个 MCP server**，工具名前缀 `mcp__<server>__*`：

| server | 工具数 | 作用 | 前提 |
|---|---|---|---|
| `awd-tools` | 10 | nmap/ffuf/nuclei/**semgrep 源码审计**/HTTP/收旗/交旗/批量执行/扫马 | 无 |
| `awd-llm` | 5 | **大模型问答 + 流量分析 + payload 复用** | 填 `traffic\llm.json` |
| `ghidra` | 30 | 反编译/交叉引用/重命名/读内存（GUI 联动） | Ghidra 打开程序 + 插件启用 |
| `radare2` | 40 | **无 GUI 反汇编/反编译/搜索/xref**，适合 pwn 快速定位 | 已配好 r2 DLL 路径 |
| `wireshark` | 19 | tshark 抓包/pcap 分析/协议统计/HTTP-DNS 解析 | 已配好 TSHARK_PATH |
| `frida` | 15 | 进程注入/动态调试/JS 脚本执行 | 目标进程存在 |
| `memory` | 9 | 知识图谱：记靶机/凭据/flag/漏洞，跨轮次不丢 | 已配 MEMORY_FILE_PATH |
| `chrome` | 30+ | 浏览器自动化 + DevTools（网络/控制台/截图/JS 执行） | 已绑 Edge 内核 |

`awd-tools` 的工具：

| 工具 | 作用 |
|---|---|
| `recon_nmap` | 端口/服务扫描 |
| `web_ffuf` | 目录爆破（用内置字典） |
| `web_nuclei` | POC 扫描 |
| `http_request` | 原始 HTTP 请求，验证漏洞/读 flag |
| `flag_collect` | 批量读所有靶机 flag |
| `flag_submit` | 直接交一个 flag |
| `target_exec` | 批量在靶机上跑命令 |
| `webshell_scan` | 扫马 |
| `semgrep_scan` | **源码静态审计**：SQLi/RCE/路径穿越/反序列化，直接给 file:line |
| `kit_info` | 自检路径与运行时 |

`awd-llm` 的工具：

| 工具 | 作用 |
|---|---|
| `llm_status` | 检查大模型 API 配置与连通性 |
| `llm_chat` | 直接问大模型（分析 payload、写 exp、解释报错） |
| `analyze_capture` | 对抓包出攻击画像 + 漏洞点 + payload（可叠加 LLM） |
| `list_payloads` | 列出可复用的高分 payload |
| `replay_payloads` | 把 payload 重放给其他队伍（需 confirm=true） |

### 用法

- 配置文件：`%USERPROFILE%\.dsh\profiles\desktop\cordis.patch.yml`（安装/卸载脚本自动备份）
- 重装：`powershell -ExecutionPolicy Bypass -File mcp\install-mcp.ps1`
- 卸载：`... install-mcp.ps1 -Remove`
- 只装部分：`... install-mcp.ps1 -Only awd-tools,awd-llm`

### Ghidra MCP 怎么用

1. `03-binary\ghidra\ghidraRun.bat` 启动（先 `. .\activate.ps1` 设好 JAVA_HOME）
2. 打开目标程序，菜单 `File → Configure → Experimental` 或 `Windows → GhidraMCP` 启用插件
3. 插件会在 `127.0.0.1:8080` 起 HTTP 后端
4. 然后就能让 DSH「反编译 sub_401000」「列出所有导入函数」

> 插件是 12.1.4 版装进 12.2，首次启用若提示版本不符，选 "Continue/忽略" 即可。

### rea（Reverse Engineer Anything）

`rea-agents 6.9.0` 已装在 `00-runtime\node-global`（255 个 MCP 工具的 CLI + MCP server）。
**默认没有注册进 DSH**——255 个工具会占掉大量上下文。需要时：

```powershell
powershell -ExecutionPolicy Bypass -File D:\AWD-Kit\mcp\enable-rea.ps1
```

它会以 `mcp__rea__*` 挂上。不想用就 `enable-rea.ps1 -Remove`。
CLI 直接用：`D:\AWD-Kit\00-runtime\node-global\rea.cmd --help`（需 node 在 PATH）。

---

## 五之二、靶机流量分析工具链（`traffic\`）

> 抓对手的 payload → 定位自己的漏洞 → 把 payload 打回去

| 文件 | 跑在哪 | 作用 |
|---|---|---|
| `capture.py` | **靶机**（root） | 纯标准库 AF_PACKET 抓 HTTP + **TLS SNI/JA3 指纹**，零依赖 |
| `deploy.sh` | **靶机** | start/stop/status/top/pack |
| `watch.py` | 本机 | **实时告警**：新 payload 出现就打印，可让大模型解释一句 |
| `analyze.py` | 本机 | 攻击画像 + 漏洞点 + payload 提取，可接大模型 |
| `replay.py` | 本机 | 改 Host 批量重放给其他队伍 |
| `llm.py` / `llm.json` | 本机 | OpenAI 兼容 API 客户端与配置 |

抓取内容：明文 HTTP 全量；TLS 只能看 SNI/ALPN/JA3（看不到内容，但 JA3 能反查对手用的扫描器）。

三步走：

```powershell
# 部署到所有靶机并启动
& $PY "$KIT\08-awd\awd.py" push -l "$KIT\traffic\capture.py" -r /tmp/.awd/capture.py
& $PY "$KIT\08-awd\awd.py" push -l "$KIT\traffic\deploy.sh"  -r /tmp/.awd/deploy.sh
& $PY "$KIT\08-awd\awd.py" exec -C "bash /tmp/.awd/deploy.sh start"

# 拿回来分析（--llm 需要先填 traffic\llm.json）
& $PY "$KIT\traffic\analyze.py" -i .\http.jsonl --llm

# 复用对手 payload 打别人
& $PY "$KIT\traffic\replay.py" -i .\http.jsonl --targets-file .\targets.txt -y
```

细节见 `traffic\README.md`。

---

## 五之三、Python 包（已装 60+）

比赛常用的一批已装进 `00-runtime\python`，直接 `import` 即可：

- **Web**：requests / httpx / bs4 / lxml / pyquery / flask / websocket-client / jsbeautifier / pyjwt / passlib
- **网络**：scapy / dpkt / pyshark / impacket / dnspython / netaddr / mmh3 / xxhash
- **二进制**：pwntools / capstone / keystone / unicorn / angr / lief / pyelftools / pefile / ropper / ROPgadget / frida
- **取证**：volatility3 / oletools / regipy / yara-python
- **密码学**：pycryptodome(x) / cryptography / gmpy2 / z3-solver / sympy
- **数据库**：pymysql / psycopg2 / pymongo / redis / sqlalchemy
- **流量**：mitmproxy / pyshark
- **代码审计**：semgrep 1.135（CLI + MCP 工具 `semgrep_scan`）

一键列出：`D:\AWD-Kit\00-runtime\python\python.exe -m pip list`

**完整清单（含版本号与用途）见 [PYTHON_PACKAGES.md](PYTHON_PACKAGES.md)**，266 个包按用途分类，并标注了不能乱升的版本。

---

## 六、Skill（已安装）

`awd-competition` 已装到 `C:\Users\Administrator\.dsh\skills\awd-competition\SKILL.md`，
DSH 会在会话技能目录里自动发现（无需重启）。
以后直接说「按 AWD 流程来」「帮我收旗交旗」「给靶机做通防」，DSH 会加载这套手册。

源文件在 `skills\awd-competition\SKILL.md`，可自行改。

---

## 七、需要你手动运行的安装包（其余全是绿色版）

| 安装包 | 路径 | 大小 | 不装会怎样 |
|---|---|---|---|
| **Npcap**（必装） | `01-recon\nmap\$PLUGINSDIR\npcap-1.90.exe` | 1.3 MB | nmap 只能 `-sT`，tshark 无法抓活包 |
| **Metasploit**（要用 msfvenom 才装） | `06-c2\metasploitframework-latest.msi` | 387 MB | 不能用 `msfvenom` 生成 payload，没有 `msfconsole` |
| **Burp Suite**（要用才装） | `02-web\burpsuite_windows-x64_v2026_11.exe` | 431 MB | 没有 Burp；可用 xpoc/sqlmap/ffuf 代替 |
| USBPcap（几乎不用） | `03-binary\wireshark\USBPcapSetup-1.5.4.0.exe` | 0.2 MB | 不能抓 USB 流量，AWD 用不上 |

安装注意：
- **Npcap** 会弹 UAC + 驱动签名确认，**没法静默装**（我试过，会卡在界面上），必须手动点。装完建议重启一次。
- **Metasploit** 装完约 1 GB，默认装到 `C:\metasploit-framework`。安装向导里如果问要不要装 Npcap，选**否**（已经装过）。
- **Burp** 是自解压安装包，双击装到默认目录即可；启动需要 JDK，先 `. .\activate.ps1`。

**完全不用装的**（双击或命令行直接用）：
nmap、ncat、fscan、kscan、httpx、nuclei、ffuf、sqlmap、dirsearch、xpoc、CyberChef(html 双击)、Ghidra、radare2、rizin、DIE、hashcat、tshark、frp、chisel、Neo-reGeorg、Venom、Stowaway、蚁剑、冰蝎、哥斯拉、Nishang、PowerCat、Sliver、ConPtyShell、Python/Node/Go/JDK/7-Zip。

**唯一需要配的环境变量**（不算安装）：`JAVA_HOME` 指向 `00-runtime\jdk`，否则 Ghidra / 冰蝎 / 哥斯拉 / Burp 起不来。跑一次 `. .\activate.ps1` 就设好了。

---

## 八、已知问题 / 注意

1. **Npcap 未安装** —— nmap 现在只能做 connect 扫描（`-sT`），tshark 不能抓活包。
   需要时手动双击安装（会弹 UAC）：
   - `01-recon\nmap\$PLUGINSDIR\npcap-1.90.exe`
   - 或 `03-binary\wireshark\npcap-1.88.exe`
   装完 nmap `-sS` 和 tshark 抓包才完整。
2. **火绒等杀软会删工具**（fscan/winPEAS/Sliver/哥斯拉是重点对象）。
   已加白名单最好；否则每次启动前把 `C:\Users\Administrator\Downloads\AWD-Kit` 加进信任目录。
3. **Ghidra / 冰蝎 / 哥斯拉** 需要 JDK，先 `. .\activate.ps1` 或手动 `set JAVA_HOME=...\00-runtime\jdk`。
4. **Metasploit** 是 MSI，未安装。要用 `msfvenom` 时双击 `06-c2\metasploitframework-latest.msi`。
5. **Burp** 安装包首次运行会释放，装到默认目录即可；需要 JDK（自带）。
6. **nuclei 首次跑**会自动下载模板到 `%APPDATA%\nuclei`，需联网。

---

## 九、更新

```powershell
# 重新拉某个工具：改 download.ps1 里的版本号/URL，然后
powershell -ExecutionPolicy Bypass -File download.ps1 -Only "ffuf"
powershell -ExecutionPolicy Bypass -File setup2.ps1
```
（`download.ps1` / `setup2.ps1` 在 `C:\Users\Administrator\Documents\deepseek-harness\default-workspace\`，
拷进 kit 根目录也能用。）

---

## 十、比赛纪律

只用于**授权的攻防比赛靶机**。脚本里的 `defense.sh --restore`、`target_exec` 会真实改目标机器状态，别对非授权目标跑。
