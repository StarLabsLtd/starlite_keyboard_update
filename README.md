# starlite_keyboard_update

This update will write a boot image to your USB stick. **Warning:** This process will delete everything on the drive.

## Steps:

### 1. Download and assemble the boot image:

Use the following commands to download the image in parts and reassemble it into a single file.

```bash
for i in $(seq -w 00 14); do
    wget "https://raw.githubusercontent.com/StarLabsLtd/starlite_keyboard_update/refs/heads/main/img_$i"
done

cat img_* > boot.img
```

### 2. Identify your USB device path:

Before proceeding, you need to identify the device path for your USB stick. Ensure the USB drive is inserted, then run:

```bash
sudo lsblk
```

Look for a device that is at least 2GB in size (e.g., `/dev/sda`, `/dev/sdb`). Make sure you correctly identify the device, as writing to the wrong one can cause data loss.

### 3. Double-check your device:

You can use the following command to get more details and verify your USB drive:

```bash
sudo fdisk -l
```

Ensure that the path you select is the correct USB drive, and remember that all data on the drive will be erased.

### 4. Write the boot image to the USB drive:

Use `dd` to write the image to your USB stick. Be extremely cautious here to avoid overwriting the wrong device.

```bash
sudo dd if=boot.img of=/dev/sdX bs=4M oflag=direct status=progress
```

Replace `/dev/sdX` with the actual device path you found in step 2.

## Important Warnings:

- Ensure you have selected the correct USB device path, as the `dd` command will erase all data on the selected drive.
- The USB stick must be at least 2GB in size to hold the full boot image.

