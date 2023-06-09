# Nat6配置助手
## 使用场景：

- 学校分配的ipv6是诸如2001:XXXX:XXXX:XXXX::XXXX:XXXX/128结尾的ip，这样就只有路由器本身能获取到公网ipv6，局域网内的设备无法得到公网ipv6。不过好歹也算是获得了公网ipv6，我们依旧可以通过类似socat等端口转发插件，实现内网穿透等等。但是要让局域网内的设备能够使用ipv6浏览网页，最好的方法还是使用nat6。  

- 本插件可以选定获取到公网ipv6的网口做nat6，并且在网络发生变化时自动更新设置。

<div align=center>
<img src="./show.png" width="480">
</div>



## 使用方法:
### 方法一（推荐）
1. 检查【系统-软件包】是否安装 `ip6tables kmod-ipt-nat6`，如若没有，请 ssh 运行 `opkg update && opkg install ip6tables kmod-ipt-nat6` 安装  

2. 到[Releases](https://github.com/StriverLite/luci-app-nat6-helper/releases)下载最新编译ipk，上传到路由器安装即可。安装教程可以参考[这个视频](https://www.bilibili.com/video/av464065982/)  

3. 在路由器管理页面的【服务】中找到nat6配置助手，首先点击一键配置按钮完成`ULA  DHCPv6  ipv6-dns服务器`的设置。本插件默认配置ULA为`fd00:6666:6666::/64`。如果想让局域网设备优先ipv6上网，可以自行在【网络-接口】处，把ULA前缀修改为`dd00::/64`

4. 稍等配置完后网络重启，完成初始化设置后，在插件设置页面勾选启用，确认选定网口与【网络-接口】有ipv6的网口名称一致，然后保存并应用即可。  

### 方法二
- 自行编译到固件内

## 参考链接：

> [hedazhong/luci-app-nat6-helper: backup (github.com)](https://github.com/hedazhong/luci-app-nat6-helper)
>
> [Ausaci/luci-app-nat6-helper: Nat6 One-Click Configuration! (github.com)](https://github.com/Ausaci/luci-app-nat6-helper)
>
> [再说 OpenWRT 校园网 IPv6 NAT6-OPENWRT专版-恩山无线论坛 - Powered by Discuz! (right.com.cn)](https://www.right.com.cn/forum/thread-2661027-1-1.html)
>
> [校园网环境下Openwrt配置ipv6教程——以nat6为例 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/492774540)
>
> [OpenWrt IPv6 NAT配置（不适合22.03⚠） (wolai.com)](https://www.wolai.com/littlenewton/nc13tvkvdazg62S2LNUKgd)
>
> [OpenWrt 配置使用 | 乐园 (ywang-wnlo.github.io)](https://ywang-wnlo.github.io/posts/51140c4a.html#ipv6)
>
> [[OpenWrt Wiki\] DNS and DHCP configuration /etc/config/dhcp](https://openwrt.org/docs/guide-user/base-system/dhcp)
