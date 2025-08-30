### 🔧 Full Rescue Sequence

```bash
# 1. Find EFI + root partitions
lsblk -f

# (assume EFI is /dev/nvme0n1p1, root is /dev/nvme0n1p3)
# adjust to match your setup!

# 2. Try to mount EFI
mount -o rw /dev/nvme0n1p1 /mnt || echo "EFI is still read-only"

# 3. If read-only, clear GPT read-only attribute
gdisk /dev/nvme0n1 <<EOF
p        # print partitions (note EFI number, usually 1)
x        # expert mode
a        # attributes
1        # EFI partition number
60       # toggle bit 60 (read-only flag)
p        # check attributes again
w        # write changes and exit
EOF

# 4. Repair filesystem just in case
fsck.vfat -a /dev/nvme0n1p1

# 5. Mount root + EFI into chroot
mount /dev/nvme0n1p3 /mnt
mount /dev/nvme0n1p1 /mnt/boot/efi
mount --bind /dev /mnt/dev
mount --bind /proc /mnt/proc
mount --bind /sys /mnt/sys

# 6. Enter chroot
chroot /mnt

# 7. Reinstall GRUB
grub2-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id="opensuse"
grub2-mkconfig -o /boot/grub2/grub.cfg

# 8. Exit and reboot
exit
umount -R /mnt
reboot
```

---

💡 After reboot, check in your firmware/BIOS boot menu — you should see **“opensuse”** again, and `/boot/efi` should mount as **rw** instead of **ro**.
