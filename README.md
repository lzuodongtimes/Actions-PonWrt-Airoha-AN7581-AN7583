Actions-PonWrt-Airoha

AN7581 XG-040G-MD

AN7583 XG-040G-MF

作者源码原样，不碰任何内核补丁。实际测试会有网速掉速问题。

PonWrt 全机型构建（作者源码 · 未改内核）
基于 pbs05/ponwrt 源码，构建 Nokia XG-040G 系列（an7581 / an7583 全部设备）固件。
这是对照基线版本：内核补丁完全保持作者原样，只做界面与打包层的要求，用来回答"某个问题是本来就有，还是我们改出来的"。
与主线相比只少一步
不删除 airoha/patches-6.18/980-revert-fraglist-gro-by-default.patch，也不新增任何内核补丁、不改 firewall.config。
因此本版本的 fraglist-GRO 保持作者默认的关闭状态，预期测速会停在 900 Mbps 左右——这是作者默认值的结果，不是故障。
仍然保留的界面/打包改动
LuCI 主题换成 Aurora
移除 LuCI「插件」页、「交换机 VLAN 配置」菜单
移除 fkwnopd / luci-app-fkwnopd（kconfig 循环依赖会阻断 make defconfig）
包名前缀 ponwrt- 改为 immortalwrt-
为 XG-040G-MD 补 ARTIFACTS 声明，使其产出 preloader.bin / bl31-uboot.fip
只编 an7581 / an7583 两个整机配置
触发方式
手动触发；每 6 小时轮询上游，仅在 pbs05 有更新时编译
带 concurrency 保护
产物
Release tag：ponwrt-stock-v<run号>
附件含 sysupgrade.itb、recovery.itb，MD 另有 preloader.bin、bl31-uboot.fip
什么时候用它
需要确认某个现象是否为上游原生问题
主线固件出问题时，用它做最小对照
想回到完全接近作者默认的固件状态
