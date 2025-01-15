# XMRig for Termux

This is a WIP repo for making XMRig and run on latest termux(v0.118.0) and latest clang(v17.0.5).

# **`Disclaimer: I accept no warranties or liabilities on this repo. Do it at your own risk!!!`**

# Installation & configuration:
1. Download & install latest arm64-v8a [Termux](https://github.com/termux/termux-app/releases/download/v0.118.0/termux-app_v0.118.0+github-debug_arm64-v8a.apk):
```
https://github.com/termux/termux-app/releases/download/v0.118.0/termux-app_v0.118.0+github-debug_arm64-v8a.apk
```
2. Installing clang and dependencies:
- Type `y` then enter key in any prompts!
```
yes | pkg update -y
yes | pkg upgrade -y
yes | pkg install build-essential binutils clang cmake git wget -y
```

3. Clone repo & chmod:
```
git clone --branch ARMv8 --single-branch https://github.com/Darktron/xmrig.git
cd xmrig
chmod +x start.sh
```

4. Compile XMRig:
```
cmake ~/xmrig && make -j$(nproc)
```
5. Compile with HWLOC
```
~/xmrig/scripts/build.hwloc.sh
cmake -DHWLOC_INCLUDE_DIR=~/xmrig/scripts/deps/include \
      -DHWLOC_LIBRARY=~/xmrig/scripts/deps/lib/libhwloc.a .
make -j$(nproc)
```

6. Change your algo, pools, address, and miner name with:
```
nano config.json
```
- Line `80` algo = your algorithm of choice.
- Line `82` url = your pool with port of choice.
- Line `83` user = your address and after can include `.Difficulty`.
- Line `84` pass = your worker name of choice.

# Usage:
1. Start ccminer with:
```
~/xmrig/start.sh
```
2. Close ccminer with:
```
CTRL + c
```
# Tips & Tricks:
- If Termux can't complete update & upgrade please clear app cache and data.
- Disable battery manager, battery optimization for Termux app.
- If you long press anywhere within Termux then click `More` there is an option to `Keep screen on`.
- Alternatively you can pull down the notification drawer and expand Termux notification to `Acquire wakelock` this will enable you to mine with the screen off **(NOTE! not all devices obey this rule is a hit or miss)**
- Use a pool with low latency to your location/internet.
- Give the miner/stratum time to stabilize hashrate(~30m-1h).
