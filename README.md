

# 🧩 MediaMTX RTSP Server Setup
>  **Official Repo:** [﻿MediaMTX GitHub](https://github.com/bluenviron/mediamtx)
**Latest Release (v1.13.1):** [﻿Download Binary](https://github.com/bluenviron/mediamtx/releases/download/v1.13.1/mediamtx_v1.13.1_linux_amd64.tar.gz) 

---

## 📁 1. Create Project Directory
```bash
mkdir mediamtx
cd mediamtx
```
---

## 📦 2. Download & Extract MediaMTX Binary
Download the precompiled Linux binary for MediaMTX:

```bash
wget https://github.com/bluenviron/mediamtx/releases/download/v1.13.1/mediamtx_v1.13.1_linux_amd64.tar.gz
tar -xzf mediamtx_v1.13.1_linux_amd64.tar.gz
```
>  This will extract the `mediamtx` binary into the current directory. 

---

## 🛠️ 3. Create MediaMTX RTSP Config File
Create a configuration file to define your RTSP streams using `vim` or any text editor:

```bash
vim mediamtx-Rtsp.yaml
```
Paste the following configuration:

```yaml
# logLevel: debug  # Uncomment for verbose logging
paths:
  Cam1:
    runOnDemand: >
      /opt/ffmpeg-2.8.8_x264_v142/bin/ffmpeg
      -re -i /video/path/name1.mp4
      -c copy -f rtsp -rtsp_transport tcp
      rtsp://0.0.0.0:$RTSP_PORT/$MTX_PATH
    runOnDemandRestart: yes
  Cam2:
    runOnDemand: >
      /opt/ffmpeg-2.8.8_x264_v142/bin/ffmpeg
      -re -i /video/path/name2.mp4
      -c copy -f rtsp -rtsp_transport tcp
      rtsp://0.0.0.0:$RTSP_PORT/$MTX_PATH
    runOnDemandRestart: yes
  Cam3:
    runOnDemand: >
      /opt/ffmpeg-2.8.8_x264_v142/bin/ffmpeg
      -re -i /video/path/name3.mp4
      -c copy -f rtsp -rtsp_transport tcp
      rtsp://0.0.0.0:$RTSP_PORT/$MTX_PATH
    runOnDemandRestart: yes
  Cam4:
    runOnDemand: >
      /opt/ffmpeg-2.8.8_x264_v142/bin/ffmpeg
      -re -i /video/path/name4.mp4
      -c copy -f rtsp -rtsp_transport tcp
      rtsp://0.0.0.0:$RTSP_PORT/$MTX_PATH
    runOnDemandRestart: yes
  Cam5:
    runOnDemand: >
      /opt/ffmpeg-2.8.8_x264_v142/bin/ffmpeg
      -re -i /video/path/name5.mp4
      -c copy -f rtsp -rtsp_transport tcp
      rtsp://0.0.0.0:$RTSP_PORT/$MTX_PATH
    runOnDemandRestart: yes
```
>  Each `CamX` path will only start streaming when accessed — thanks to `runOnDemand`.
Replace `$RTSP_PORT` and `$MTX_PATH` with actual values or environment variables. 

---

## 🚀 4. Start the MediaMTX Server
Run the server with your custom config:

```bash
./mediamtx mediamtx-Rtsp.yaml
```
Once started, you can connect to streams like:

```
rtsp://<server-ip>:8554/Cam1
rtsp://<server-ip>:8554/Cam2
...
```
>  The default RTSP port is `8554`, unless overridden. 

---



