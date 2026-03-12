3/11/26

# Today I installed NixOS on a dual boot for my first time


Typically I use a vm to access linux. I wanted to dual boot linux since windows 10 support ended, however, wanting to work with cloud projects (especially KubeVirt for GSoC 2026) made me stop postponding this task.


---

First I had to backup my drive incase anything were to happen. The drive was formated by my mac, so I had to wipe the drive and reformat it to match the window system.

After that I shrunk the main partition down a bit. I made a 500 MB EFI partition for booting and a 350GB partition for nixos. 

I had to update my file system on my windows since it was mbr (outdated) and I needed gpt fs to access uefi for dual booting.

I used the powershell tool mbr2gpt, it comes with a validation flag which is nice to use before converting your files, I think it actually saved me.

After that I flashed a basic (no gui) nixOS onto my flashdrive with rufus


