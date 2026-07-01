# DeltaruneChineseLinuxPackaging

提供了一个补丁来为 [好人汉化组的 DELTARUNE 中文本地化补丁](https://github.com/gm3dr/DeltaruneChinese) 提供非官方的Linux补丁构建支持

## ❗ 新补丁脚本
我发现 [DeltaruneChinese](https://github.com/gm3dr/DeltaruneChinese) 代码库更新速度太快，以至于补丁太容易失效了，所以我打算写一个补丁脚本来解决这个问题

如果补丁文件失效了，可以自己按改动内容的



## 🤔 改动内容

1. 将`5-生成汉化补丁.ps1`脚本所有路径的 `\` 符号改为了 `/` ，来解决调用部分第三方工具时找不到路径的问题
2. 改动了在 Linux 下 Steam 存放游戏本体目录的位置
3. 对于 `bmfont64.exe` 则使用 Wine 来运行它，而其它工具则全部使用系统自带的
4. 在构建汉化补丁时，不生成自解压版安装程序，类似 Linux 的打包版本

## 🔨 使用

1. 复制本仓库的 `LinuxPackaging.patch` ，并应用补丁:

```bash
# 假设你把补丁文件放在了 gm3dr/DeltaruneChinese 仓库的根目录
git apply LinuxPackaging.patch
```

2. 安装相关工具（若已安装可以跳过）:

```bash
# Debian / Ubuntu / 其它 Debian 系发行版
sudo apt install xdelta3 7zip curl npm nodejs wine
## Ubuntu 在官方仓库有 .NET SDK ，所以需要额外执行:
sudo apt install dotnet-sdk
## Debian 安装 .NET SDK 参考 https://learn.microsoft.com/zh-cn/dotnet/core/install/linux-debian

# Fedora / RHEL / 其它 Fedora 系发行版
sudo dnf install xdelta 7zip curl npm nodejs dotnet-sdk wine

# Arch Linux / Arch Linux ARM / Manjaro / CachyOS / 其它 Arch 系发行版
sudo pacman -S xdelta3 7zip curl npm nodejs dotnet-sdk wine
```

3. 去 [PowerShell Github](https://github.com/PowerShell/PowerShell/releases/latest) 安装PowerShell并把它们放到Path变量里

    - 若你使用的是 Arch 系发行版，可以使用AUR安装它（这里使用`yay`作为其中一个AUR助手的示例）:

```bash
# 主线版本
yay -S powershell-bin

# LTS 版本
yay -S powershell-lts-bin

# 预览版本
yay -S powershell-preview-bin
```

4. 填充 `/patcher` 目录为以下内容:

    - 其中，这些文件可以在 [gm3dr/DeltaruneChinesePatcher](https://github.com/gm3dr/DeltaruneChinesePatcher/releases/latest) 仓库里取得

```text
./patcher
├── linux
│   └── Linux 补丁安装器
├── win
│   └── Windows 补丁安装器
└── winold
    └── Windows 旧版补丁安装器
```

5. 根据原仓库的 [工作流简介](https://github.com/gm3dr/DeltaruneChinese#%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%AE%80%E4%BB%8B-powershell-%E8%84%9A%E6%9C%AC) 构建补丁

    - 但是，这些PowerShell脚本需要以下面的方式来运行
    - 其中， `*.ps1` 为脚本路径

```bash
pwsh ./*.ps1 
```

## ⚠️ 免责声明

这个补丁是非官方的，并不能代表好人汉化组以及Toby Fox的意见，这只是我的一个业余项目，可能会有随时弃坑的风险，使用风险自己承担
