---
vendor: sipeed_licheepi4a
product: LicheePi 4A
cpu: TH1520
cpu_core: XuanTie C910 + XuanTie C906 + XuanTie E902
---

# Lichee Pi 4A

## Testing Environment

### System Information

- openEuler RISC-V 24.03 Preview
    - Download Link: https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/testing/2403LTS-test/v1/lpi4a/
    - Reference Installation Document: https://docs.openeuler.org/zh/docs/24.03_LTS/docs/Installation/RISC-V-LicheePi4A.html
- RevyOS 20240110
    - Download link: [RevyOS Images](https://mirror.iscas.ac.cn/revyos/extra/images/lpi4a/)
    - Reference Installation Document: [RevyOS Documentation](https://docs.revyos.dev/)
- openKylin 2.0 SP1
    - Download link: [OpenKylin Downloads](https://www.openkylin.top/downloads/index-cn.html)
    - Reference Installation Document: [OpenKylin Installation Guide](https://docs.openkylin.top/zh/01_%E5%AE%89%E8%A3%85%E5%8D%87%E7%BA%A7%E6%8C%87%E5%8D%97/%E5%9C%A8riscv%E4%B8%8A%E5%AE%89%E8%A3%85/%E5%9C%A8LicheePi4A%E4%B8%8A%E5%AE%89%E8%A3%85openKylin)
- Fedora 38
    - Download link: [Fedora Images](https://openkoji.iscas.ac.cn/pub/dl/riscv/T-Head/th1520_light/images/)
    - Reference Installation Document: [Fedora Installation Guide](https://fedoraproject.org/wiki/Architectures/RISC-V/T-Head)
- Armbian (Ubuntu 20.04 LTS)
    - Download link: [Armbian Images](https://github.com/chainsx/armbian-riscv-build/tree/main)
    - Reference Installation Document: [Armbian Installation Guide](https://github.com/chainsx/armbian-riscv-build/blob/main/doc/licheepi-4a-install-guide.md)
- Arch Linux
    - Download link: [https://mirror.iscas.ac.cn/archriscv/images/](https://mirror.iscas.ac.cn/archriscv/images/)
    - Reference Installation Document: 
    - [ArchWiki](https://wiki.archlinux.org/title/General_recommendations)
- Deepin preview 20240603
    - Download link: https://cdimage.deepin.com/RISC-V/preview-20240613-riscv64/deepin-23-beige-preview-riscv64-lpi4a-20240613-122949.tar.xz
    - Reference Installation Document: https://cdimage.deepin.com/RISC-V/preview-20240517-riscv64/

### Hardware Information

- Lichee Pi 4A 16GB RAM + 128GB eMMC
- Lichee Pi 4A 8GB RAM + 32GB eMMC

## Test Results

| Software Category             | Software Package | Test Results (Test Report)              |
| ----------------------------- | ---------------- | --------------------------------------- |
| openEuler/Base Image Boot     | N/A              | [Success][oERV]                         |
| openEuler/Xfce Image Boot     | Xfce             | [Success][oERV]                         |
| RevyOS Desktop Image Boot     | N/A              | [Success][RevyOS] (Official Support)    |
| Fedora Desktop Image Boot     | N/A              | [Success][Fedora] (Official Support)    |
| openKylin Desktop Image Boot  | N/A              | [Success][openKylin] (Official Support) |
| Armbian (Ubuntu) Image Boot   | N/A              | [Success][Armbian]                      |
| OpenWRT Image Boot            | N/A              | [Success][OpenWRT]                      |
| Arch Linux Desktop Image Boot | N/A              | [Success][ArchLinux]                    |
| Deepin Desktop Image Boot     | N/A              | [Success][Deepin]                       |

[oERV]: ./openEuler/README.md
[RevyOS]: ./RevyOS/README.md
[Fedora]: ./Fedora/README.md
[Armbian]: ./Armbian/README.md
[openKylin]: ./openKylin/README.md
[OpenWRT]: ./OpenWRT/README.md
[ArchLinux]: ./ArchLinux/README.md
[Deepin]: ./Deepin/README.md
