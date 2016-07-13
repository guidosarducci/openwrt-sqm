SQM Package Repository for LEDE

Includes:
kmod-sched-cake
tc-adv
sqm-scripts

Build instructions:

1. Get LEDE project trunk buildroot:
`git clone git://github.com/lede-project/source.git`

2. Move in newly created folder:
`cd source`

3. Create a custom feed by copying the default file and add the sqm repository:
   ```
   cp feeds.conf.default feeds.conf
   echo "src-git sqm https://github.com/antoinedeschenes/openwrt-sqm.git" >> feeds.conf
   ```
   
4. Update and install all packages coming from feeds, with this feed first: 
   ```
   ./scripts/feeds update -a
   ./scripts/feeds install -p sqm -a
   ./scripts/feeds install -a
   ```
   
5. Configure LEDE build with `make menuconfig`, select the proper router target 
   and ensure the following packages are present:
   ```
   Luci->Collections->luci
   Luci->Applications->luci-app-sqm
   Kernel Modules->Network Support->kmod-sched-cake
   Network->Routing & Redirection->tc-adv
   ```
   
6. Build the firmware with `make`. Images are in the `bin/PLATFORM` directory.

Original instructions from bufferbloat.net:
http://www.bufferbloat.net/projects/codel/wiki/Cake
