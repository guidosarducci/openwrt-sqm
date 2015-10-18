Package Repository for OpenWrt

Allows to easily add sch_cake and sch_fq_pie to an OpenWrt trunk buildroot.

Includes:
kmod-sched-cake
kmod-sched-fq_pie
tc-adv
sqm-scripts

Build instructions:

1. Get OpenWrt trunk buildroot:
`git clone git://git.openwrt.org/openwrt.git`

2. Move in newly created folder:
`cd openwrt`

3. Make a custom feed file and add the sqm feed:
   ```
   cp feeds.conf.default feeds.conf
   echo "src-git sqm https://github.com/antoinedeschenes/openwrt-sqm.git" >> feeds.conf
   ```
   
4. Update and install all packages from all standard and the sqm feed: 
   ```
   ./scripts/feeds update -a
   ./scripts/feeds install -p sqm -a
   ./scripts/feeds install -a
   ```
   
5. Configure OpenWrt build with `make menuconfig`, select the proper router target 
   and make sure to add the following packages at a minimum:
   ```
   Luci->Collections->luci
   Luci->Applications->luci-app-sqm
   Kernel Modules->Network Support->kmod-sched-cake
   Kernel Modules->Network Support->kmod-sched-fq_pie
   Network->Routing & Redirection->tc-adv
   ```
   
6. Build the firmware with `make`. Images are in the `bin/PLATFORM` directory.

Original instructions for the ceropackages-3.10 repository:
http://www.bufferbloat.net/projects/codel/wiki/Cake
