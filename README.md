<div align="center">
  <img src="assets/icon.png" width="88" alt="镜匣 DiskCoffer" />
  <h1>镜匣 · DiskCoffer</h1>
  <p><strong>不启动虚拟机，也能检查、修复、改密和迁移镜像。</strong><br />
  源文件始终只读，所有修改都交付为新镜像。</p>
  <p>
    <a href="https://github.com/yanxinwu946/diskcoffer/releases/latest"><img src="https://img.shields.io/github/v/release/yanxinwu946/diskcoffer?style=flat-square&label=release" alt="Latest release" /></a>
    <img src="https://img.shields.io/badge/Windows-x64-0078D4?style=flat-square&logo=windows11&logoColor=white" alt="Windows x64" />
    <img src="https://img.shields.io/badge/Linux-x64-FCC624?style=flat-square&logo=linux&logoColor=black" alt="Linux x64" />
    <img src="https://img.shields.io/badge/macOS-arm64-000000?style=flat-square&logo=apple&logoColor=white" alt="macOS arm64" />
  </p>
</div>

---

镜匣把虚拟机镜像变成可离线操作的工作区：打开镜像就能看卷、系统和文件，把改密、改配置、写文件放进同一个队列，最后统一校验并生成新镜像。原始文件不动，交付结果可以随时回退。

## 下载

| 平台 | 运行文件 | 说明 |
| --- | --- | --- |
| Windows x64 | `diskcoffer.exe` | 直接运行，包内已包含 ext 日志恢复组件 |
| Linux x64 | `diskcoffer` | 需要桌面图形运行环境 |
| macOS Apple Silicon | `DiskCoffer.app` | 临时签名，未提交 Apple 公证 |

从 [Releases](https://github.com/yanxinwu946/diskcoffer/releases/latest) 下载对应平台的压缩包，完整解压后运行。每次发布附带 `SHA256SUMS.txt` 校验清单。

Linux / macOS 的 ext 日志恢复使用系统 `e2fsck`；OVA 导出需要 `VBoxManage`，QCOW2 读写需要 `qemu-img`。路径可在「设置与外观 → 工具链」中检查和配置。

## 适合这些场景

- OVA 从 VirtualBox 换到 VMware 后导入失败，或开机拿不到 IP
- 一批实验镜像需要统一改密
- 关机镜像里查找 flag、配置或账户痕迹
- 整理快照链，导出一块可以独立交付的磁盘

## 主要能力

| 能力 | 说明 |
| --- | --- |
| 镜像工作区 | 一个窗口看清磁盘、分区、系统和文件，不用启动客户机 |
| 批量改密 | 一次选择多台镜像，自动定位 Windows 管理员或 Linux root，逐台生成并校验新镜像 |
| 内容搜索 | 关机状态也能按文件名或内容搜索整卷，适合排查配置和离线取证 |
| 更改队列 | 改密、写文件、改配置按顺序排队，最后一次性应用，减少反复导出 |
| 跨平台交付 | 直接产出 VMware Workstation、VirtualBox、Proxmox VE、KVM 可用的独立磁盘 |
| Windows 哈希 | 离线读取本地账户和域账户的 NT/LM 哈希，结果只在本机显示 |
| 快照链 | 理清父盘依赖，导出不依赖原链的独立磁盘 |
| 使用体验 | 原生文件选择器、浅色 / 深色 / 跟随系统、桌面与移动端自适应 |

## 三步完成

1. **导入镜像**：只读检查卷、系统和可操作项，源文件保持不变。
2. **排队修改**：改密、写入、编辑、重命名、删除按顺序加入队列。
3. **校验交付**：应用后回读校验，生成新镜像，原镜像保留作回退。

## 支持的格式

| 项目 | 格式 |
| --- | --- |
| 读取 | OVA、VMDK、VDI、VHD、VHDX、QCOW2、RAW |
| 输出 | VMDK、OVA、VDI、VHD、VHDX、QCOW2、RAW |
| 交付目标 | VMware Workstation、VirtualBox、Proxmox VE、KVM |

VMDK 可直接挂载；OVA 带 SHA-256 清单，VirtualBox 和 VMware 均可导入；QCOW2 通过 QEMU 读写。

## 系统要求

- Windows x64：主流 Windows 桌面环境
- Linux x64：桌面图形环境，需系统图形运行库
- macOS Apple Silicon：临时签名，未提交 Apple 公证

## 已知限制

- Windows 改密支持本地 SAM 账户，要求干净的 SAM；BitLocker 卷可识别，解锁需在外部完成。
- 任意文件写入和多步队列目前只支持 ext 卷；NTFS 支持浏览、导出和独立的 SAM 改密。
- 快照链操作前请关停虚拟机，并授权包含整条链的目录；虚拟机级快照管理仍需在虚拟化平台内完成。
- 转换只复制磁盘内容，不保证操作系统驱动跨平台兼容；Windows 换平台后可能需要调整磁盘控制器驱动。

## 反馈

使用中遇到问题或有功能建议，请到 [Issues](https://github.com/yanxinwu946/diskcoffer/issues) 提交，并附上镜像格式、平台和复现步骤。

## 许可说明

本软件包含第三方组件，其许可文本随发布包提供。
