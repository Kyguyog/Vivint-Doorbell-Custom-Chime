# Replacing the Chime on Vivotek DB8331W (Vivint Doorbell)

## Requirements

- lftp installed on your computer
- ffmpeg installed on your computer
- Your doorbell's IP address and root credentials
- Your replacement audio file (any format ffmpeg can read)

## Step 1: Convert Your Audio File

The device requires a very specific WAV format. Use this exact ffmpeg command:

```bash
ffmpeg -i yourcustom.mp3 -ar 8000 -ac 1 -acodec pcm_s16le -bitexact -fflags +bitexact -map_metadata -1 bell.wav
```

## Step 2: Connect via FTP

```bash
lftp root@192.168.1.36
```

Use your root password when prompted.

## Step 3: Navigate to the Audio Directory

```bash
cd /mnt/flash/etc/audioclip
```

## Step 4: Upload and Set Permissions

```bash
put bell.wav bell.wav
chmod 644 bell.wav
```

## Step 5: Test

Press the doorbell button. The new chime should play immediately with no reboot required.

