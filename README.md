<p align=center>
    <img src="img/icon.png" width="200" alt="Pi 4b latency demo">
</p>
<h1 align="center">
 Pi Camera
 <br>
</h1>

<p align=center>
<a href="https://play.google.com/store/apps/details?id=com.tzu.huan.tai.picamera"><img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" width="168"></a>
</p>

Transform your Raspberry Pi into a powerful home security camera — with low-latency live streaming, playback support, and full P2P privacy. Built using [`picamera-react-native`](https://www.npmjs.com/package/picamera-react-native), this app connects directly to your Raspberry Pi camera over WebRTC and MQTT — no complex backend required.

🎥 [Watch demo](https://www.youtube.com/watch?v=JZ5bcSAsXog)

<img src="./img/index_dark.png" width="30%"> <img src="./img/live_dark.jpg" width="30%"> <img src="./img/records_dark.jpg" width="30%">

# Key Features

👉 **Low-Latency Live Monitoring**: Achieve extremely low-latency video streaming through WebRTC technology, ensuring you don’t miss any important moments.

👉 **Playback of Historical Footage**: Easily view and manage recorded videos to meet your security needs.

👉 **Simple Setup**: Quickly configure your Raspberry Pi camera through a user-friendly interface.

👉 **Privacy Protection**: Direct P2P connection without relying on third-party servers ensures that your data is fully under your control.

👉 **Open-Source Support**: The camera source code is fully open-source, allowing you to customize and extend it as needed.

# Setting Up a New Raspberry Pi

## Step 0: Prerequisites

1. A Raspberry Pi with a camera module attached.
2. A MQTT server. (STUN and TURN servers are optional).

    <img src="./img/pi_zero_wi_shell.jpg" width=30%> <img src="./img/pi_zero_wo_shell.jpg" width=30%><br>

> [!IMPORTANT]
> - **MQTT Server (necessary)**: **Must support SSL/TLS!** Used for exchanging initial WebRTC signaling (ICE, SDP). Match this with your Raspberry Pi setup.
Consider providers like [HiveMQ](https://www.hivemq.com), [EXMQ](https://www.emqx.com/en).
> - STUN Server (optional): Defaults to `stun:stun.l.google.com:19302` if left blank.
> - TURN Server (optional): Helps in NAT-restricted networks when P2P is not possible.

## Step 1: Set Configurations on the App

1. Go to Setting Page.
2. Tap the 🌐 icon and paste your MQTT & signaling configuration.
Here is an example mqtt setting shown on HiveMQ.

> [!IMPORTANT]
> Please use ***WebSocket Port*** here!


<img src="./img/mqtt_cloud_sample.jpg" width=50%><br>
<img src="./img/setting_1.jpg" width="30%"> <img src="./img/setting_2.jpg" width="30%">

## Step 2: Add a New Device

1. Tap the ➕ icon.
2. The app generates a `UUID`, used by your Raspberry Pi. You can modify it before saving.
3. Enter an alias (editable anytime).
4. Confirm to add the device. Drag ☰ icon to reorder.

    <img src="./img/add_devices.jpg" width="30%">

## Step 3: Run Camera Software on Raspberry Pi

1. Download the `pi_webrtc` from the [release page](https://github.com/TzuHuanTai/RaspberryPi_WebRTC/releases).

2. Run with your device's `UUID` and MQTT credentials.

> [!IMPORTANT]
> MQTT port used in command = 8883 (**not** the WebSocket port).

```bash
./pi_webrtc \
    --camera=libcamera:0 \
    --fps=30 \
    --width=1280 \
    --height=960 \
    --use_mqtt \
    --mqtt_host=your.mqtt.cloud \
    --mqtt_port=8883 \
    --mqtt_username=xxxx \
    --mqtt_password=xxxx \
    --uid=your-generated-uid \
    --no_audio \
    --hw_accel # --hw_accel only for Pi zero 2w, 3b, 3b+, and 4b. Remove it for Pi 5.
```

Refer to [RaspberryPi-WebRTC](https://github.com/TzuHuanTai/RaspberryPi-WebRTC) for full setup guide.

## Step 4: Verify the Connection

- Open the home page.

- A green status light means connection is live.

- Preview refreshes every 90 seconds or manually by pull-to-refresh.

    <img src="./img/connected_sample.jpg" width="30%">


## Step 5: Share to Other Phones

1. Tap the share button to display QR code.

2. On the second phone, scan the QR code in the add device section.

> [!WARNING]
> The network setting will be replaced in the second phone if set before.

<img src="./img/share_1.jpg" width="30%"> <img src="./img/share_2.jpg" width="30%">
