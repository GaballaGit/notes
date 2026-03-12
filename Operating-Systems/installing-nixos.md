3/11/26

# Today I installed NixOS on a dual boot for my first time


Typically I use a vm to access linux. I wanted to dual boot linux since windows 10 support ended, however, wanting to work with cloud projects (especially KubeVirt for GSoC 2026) made me stop postponding this task.


---

First I had to backup my drive incase anything were to happen. The drive was formated by my mac, so I had to wipe the drive and reformat it to match the window system.

After that I shrunk the main partition down a bit. I made a 500 MB EFI partition for booting and a 350GB partition for nixos. 

I had to update my file system on my windows since it was mbr (outdated) and I needed gpt fs to access uefi for dual booting.

I used the powershell tool mbr2gpt, it comes with a validation flag which is nice to use before converting your files, I think it actually saved me.

After that I flashed a basic (no gui) nixOS onto my flashdrive with rufus.

Into the boot menu, I had to change my bios to UEFI, as well as some other changes to boot the usb. I don't exactly remember what I did here (I think I disabled some sort of dual boot security)

Fast forward a bit, I boot nixOS with my usb. Started off with sudoing myself to do anything, I check if my internet was okay with ip a. Looked like it was, After that was formating the partitions I made. I actually decided to make one more partition here because I wanted a swap partition with my nixos.

Some useful tools I used:
* lsblk - list block. Gave me information about the disk block, I mainly used it to see what was up with my /dev/sda's
* parted - Allowed modification to the disk partitions, I used this to created my nixos swap drive, as well as print out flag information of each partition. Useful for helping me debug boot later. It was also super important for setting partition flags.
* swaplabel - cause I wanted to give my swaps unique names

after formating the partitions, I had to initalize the configuration.nix file. It was intresting to see what I wanted to enable and disable in my configueration, and it was very easy compared to other systems in my opinion. Soon I will probably switch to a flake based layout, but thats going to be for when I am more familar with this OS.

finally I ran `nixos-install` and than reboot, and was in.

---

## Some issues I ran into
* /dev/sda1 was my efi patition the one used to boot. However it was a unaccepted file format, I forgot which one but I had to convert it to FAT32 with `mkfs.fat -F32 /dev/sda1`.
* Another issue with my efi was I wasn't setting the correct flags. I was trying to use parted set boot with the efi partition, but that didn't work (spoiler, since it was a windows partition). The flag esp ended up working. 

it was a suprisingly smooth experience, granted it did take most of the day, but I am happy.
