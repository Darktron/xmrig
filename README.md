# XMRig for Termux

This is a WIP repo for making XMRig v6.25.0 and run on latest termux(v0.118.3) and latest clang(v21.1.8).

# **`Disclaimer: I accept no warranties or liabilities on this repo. Do it at your own risk!!!`**

# Installation & configuration:
1. Download & install latest arm64-v8a [Termux](https://github.com/termux/termux-app/releases/download/v0.118.3/termux-app_v0.118.3+github-debug_arm64-v8a.apk):
```
https://github.com/termux/termux-app/releases/download/v0.118.3/termux-app_v0.118.3+github-debug_arm64-v8a.apk
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
mkdir ~/xmrig/build
cd ~/xmrig/build
chmod +x ~/xmrig/start.sh
```

4. Compile XMRig:
```
cmake ..
make -j$(nproc)
mv xmrig-notls xmrig
strip ~/xmrig/xmrig
```

5. Change your algo, pools, address, and miner name with:
```
nano config.json
```
- Line `62` algo = your algorithm of choice.
- line `63` coin = coin of choice (optional).
- Line `64` url = your pool with port of choice.
- Line `65` user = your address and after can include `.Difficulty`.
- Line `66` pass = your worker name of choice.

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
