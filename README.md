# Replacing the Chime Sound on Vivotek DB8331W (Vivint Doorbell)

## Requirements

- ffmpeg installed on your computer
- Your doorbell's IP address and root credentials (should be root:adcvideo)
- Your replacement audio file (theoretically any format ffmpeg can read)

## Convert Your Audio File

The device requires a very specific WAV format. Use this exact ffmpeg command (besides the input filename):

```bash
ffmpeg -i yourcustom.mp3 -ar 8000 -ac 1 -acodec pcm_s16le -bitexact -fflags +bitexact -map_metadata -1 bell.wav
```


## Upload

Choose either method:

<details>
<summary><strong>Option A: Command Line (FTP)</strong></summary>

## Connect via FTP (Use YOUR DOORBELL'S ip addr)

```bash
lftp -u root,adcvideo 192.168.1.36
```

## Navigate to the Audio Directory

```bash
cd /mnt/flash/etc/audioclip
```

## Upload the file to the dir

```bash
put bell.wav /mnt/flash/etc/audioclip/bell.wav
```

</details>

<details>
<summary><strong>Option B: Web UI</strong></summary>

**Enable web access** — paste this URL into your browser (replacing the IP with your doorbell's):

```
http://[your-cam-ip]/cgi-bin/admin/setparam.cgi?network_http_webaccess=1
```

**Open the firmware/file upload page:**

```
http://[your-cam-ip]/setup/system/maintain.html#tabs-2
```

**** Click **Choose File**, select your converted `bell.wav`, then click **Upload**.

That's it — no reboot needed.

</details>

## Step 5: Test

Press the doorbell button. The new chime should play immediately with no reboot required.
