# 看板

## 参考

## current

* laptop 🗄 `km.md` `vim.md`

## next

* backup: jazz 20s-40s after rf
* move email away from Google

music mgmt
- [ ] rf music library
- [ ] get new phone with more storage

## done

* _22_: port from `linux.md`

# DR

terminology
* _backup_: user files
* _image_: OS
* _bootable disk_: disk from which OS can boot https://pc.net/helpcenter/answers/startup_disk_vs_bootable_disk
* _startup disk_: disk from which OS actually does boot https://pc.net/helpcenter/answers/startup_disk_vs_bootable_disk
* _SD card_: non-volatile memory i.e. really fast storage
* _flash_: write OS image (to SD card) https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=24621 https://uglyduck.ca/linux-mint-macbook-air/

things that might break if you wiped your machine
* licenses: Ableton, Sound Source, Human Japanese
* VS Code: outline broken on newer version, idk if Markdown extensions work on newer versions

---

https://bsago.me/posts/lessons-learned-when-my-ssd-died

env setup order
* Homebrew
* git
* pyenv
* nvm

backups
* DR: ports
* scenario planning
* file sync

> taxonomy: runbook (manual file backup), reimage (os backup), foo_file_service_backup

https://blog.codepen.io/2014/05/27/013-backups/ https://drewdevault.com/2020/04/22/How-to-store-data-forever.html https://news.ycombinator.com/item?id=28758415
* _bootable drive_: `install macOS Mojave` in large safe 🔗 'OS versions'
* _data recovery_: https://news.ycombinator.com/item?id=8058818
* _deduplication_: only touch new data (vs. entire file)
* _hard drive health stats_: https://news.ycombinator.com/item?id=11110902 https://en.wikipedia.org/wiki/S.M.A.R.T. https://superuser.com/questions/1037644/samsung-ssd-wear-leveling-count-meaning

## backup

|  item           | location | date  | contents                         | to            |
|-----------------|----------|-------|----------------------------------|---------------|
| digits          | `zvmac`  | 19.07 | pw                               | safe, lockbox |
| phone           | -        | 22.03 | pictures, msgs                   | `zvmac`       |
| calendar        | -        | 22.10 |                                  | `zvmac`       |
| email           | -        | 22.01 |                                  | `ExFatMain`   |
| `zvmac`         | mac      | 22.10 | `jay` `sw` `za`                  | `ExFatMain`   |
|                 |          | 22.10 |                                  | Dropbox       |
| `music-usb`     | mac      | 22.10 | music                            | `ExFatMain`   |
|                 |          | 22.?  |                                  | Dropbox       |
| `Exfat-Main`    | flat     | 22.04 | `zvmac` + docs, exported, media  | `WD1`         |
|                 |          | 22.10 |                                  | Dropbox       |
| `WD1`           | safe     | 19.08 | `Exfat-Main`                     | `WD2`         |
| `WD2`           | lockbox  | 20.06 | `WD1`                            |               |

---

latin
gospel piano
the band

recent
* phone
* desktop

potential new config
> same price as Dropbox but with incremental for local files
* $7.50 - Tarsnap for `zvmac` https://www.tiltedwindmillpress.com/product/tarsnap-mastery-online-backups-for-the-truly-paranoid/ https://www.kalzumeus.com/2014/04/03/fantasy-tarsnap/
* $3.00 - Google Drive for music
* $0.00 - personal drives

🎗 now that you're copying music files btw work machine and music-usb
* backup music-usb to exfat-main
> 22.02.10
* backup exfat-main non music files to new hard drive
* backup exfat-main music files to other drives and Dropbox
* now you can transfer work machine music files back
* this way if your work machine corrupts the files somehow you have physical and cloud backups of everything before that

recently updated
> 🎗 use music-lib for easier backups!
> do mac journal
* digits
* moved to ExFatMain: comedy, training

physical storage
* keys: office desk
* safe: HD, passport, personal
* lockbox: HD, personal

---

* regularize email export https://news.ycombinator.com/item?id=29978099
* https://hacker-tools.github.io/backups/
* https://unixsheikh.com/articles/how-i-store-my-files-and-why-you-should-not-rely-on-fancy-tools-for-backup.html
* export addresses from Amazon
* preventing file corruption https://duckduckgo.com/?q=how+do+hard+drives+get+corrupted&atb=v161-1&ia=web
* defrag?

Backblaze https://wesbos.com/uses
📙 Shotts command line ch. 18
* ❓ versioned backups to prevent data corruption? https://hacker-tools.github.io/backups/
* 📍 extra consideration to code (dupe to Gitlab), digits, email https://hacker-tools.github.io/backups/ https://kevq.uk/i-nearly-lost-all-of-my-data/ 
* weird files on backup drives http://blog.hostilefork.com/trashes-fseventsd-and-spotlight-v100/

terms
* _transfer_: point A to B
* _sync_: transfer but periodic/continuous https://kevq.uk/building-my-home-server https://syncthing.net/
* _backups_: sync w/ versioning?

sync
> taxonomize
* `rsync -rv --exclude=.git <dir> <path/to>` https://stackoverflow.com/a/3672584/6813490
* syncthing https://tonsky.me/blog/syncthing/
* BackupPC https://backuppc.github.io/backuppc/
* Dropbox https://superuser.com/q/351169/728972
* Own Cloud, Amazon Glacier, BackBlaze, Arq https://github.com/kahun/awesome-sysadmin#backups https://github.com/rclone/rclone
* _local_: Restic https://github.com/restic/restic Borg https://www.borgbackup.org/ https://news.ycombinator.com/item?id=13694079 
* rclone https://news.ycombinator.com/item?id=22082585 http://www.cis.upenn.edu/~bcpierce/unison/ https://news.ycombinator.com/item?id=22791036
* Perkeep/Camlistore https://news.ycombinator.com/item?id=23676350
* Backblaze https://news.ycombinator.com/item?id=26426489
* https://news.ycombinator.com/item?id=26902422 https://github.com/rclone/rclone
* https://github.com/sahib/brig

transfer
* _FTP_: sends raw binary instead of metadata
* client (FileZilla) server (VSFTPD)
* GUI for server https://github.com/mickael-kerjean/filestash https://blog.devgenius.io/tired-of-the-modern-web-discover-some-retro-protocols-you-still-can-use-today-30bbca48d3f2
* _scp_: https://en.wikipedia.org/wiki/Secure_copy
* insecure?  https://goteleport.com/blog/scp-familiar-simple-insecure-slow/
```sh
# to remote https://haydenjames.io/linux-securely-copy-files-using-scp/
scp /local/file.txt user@host:/src
# from remote
scp user@host:/src/file.txt /local/
```
* _SFTP_: FTP + security https://github.com/drakkan/sftpgo https://goteleport.com/blog/scp-familiar-simple-insecure-slow/
* magic wormhole https://www.youtube.com/watch?v=oFrTqQw0_3c
* rsync https://goteleport.com/blog/scp-familiar-simple-insecure-slow/ https://missing.csail.mit.edu/2019/remote-machines/ impl https://news.ycombinator.com/item?id=31958536
```sh
# sync local to remote
rsync --rsync-path 'sudo -u app rsync' -arvR --exclude '.*' --exclude '*~' .  ${DEST_HOST}:/opt/t3  # start
fswatch --recursive --one-per-batch . | xargs -L1 -II rsync --rsync-path 'sudo -u app rsync' -arvR --exclude '.*' --exclude '*~' .  ${DEST_HOST}:/opt/t3 # on file change
```

Time Machine
* backup https://support.apple.com/en-us/HT201250
* restore https://support.apple.com/en-us/HT203981
* slow?
> There are only a few issues I can think of with Time Machine: first, it can slow things down on older, less powerful Macs. Five to ten years ago, it was common for my consulting clients to refuse to use Time Machine because they were tired of watching it slow down their machines. The other issue? Time Machine backups aren’t bootable — in other words, you can’t just select the backup drive during bootup and use it to bring a machine with a dead primary drive back to life. You can, however, boot from the Mac recovery partition and attempt to restore your machine with the backup. - https://blog.macsales.com/29785-backup-month-a-look-at-time-machine-carbon-copy-cloner-superduper
* deletion: should be automatically purged as they age and as the drive space dips; can do manually https://www.macworld.com/article/3260635/macs/how-to-delete-time-machine-snapshots-on-your-mac.html https://www.youtube.com/watch?v=GYXOuP6_PSQ
* list: `tmutil listlocalsnapshotdates` https://forums.macrumors.com/threads/how-to-delete-time-machine-local-backups-on-high-sierra.2073998/
* filepath: on my machine stored in `Volums/.com.apple.TimeMachine.localsnapshots` https://robservatory.com/disable-local-time-machine-backups-on-laptops/
* can always disable TM backups from System Preferences, which will start clearing out local backups

## reimage

🗄 setup

factory reset
* aka "Erase all contents and Settings"
> iOS where instead of going through this process it will just wipe everything and put a clean copy of macOS just like a fresh install just without the hassle of booting from drive etc. https://www.youtube.com/watch?v=rgHyvj_nWCU
* hardware: M1, T2 from 2017
* available from System Preferences
* _system partition_: os https://www.youtube.com/watch?v=O882iWxtZyo 2:50
* _data partition_: user files, settings
* after reset leave at Activate Mac screen otherwise will save your wifi to settings https://www.youtube.com/watch?v=O882iWxtZyo 3:15
* after Activate Mac, just reset to Setup Assistant

create image https://www.youtube.com/watch?v=rgHyvj_nWCU
* download OS version in App Store
* quit out of install
* format drive using Disk Utility to "Mac OS Extended Journaled"

test reimage
* create image
* add couple of apps/files
* reimage
* verify only apps/files from basic set up

---

* _storage cleanup_: https://www.macworld.com/article/2030221/macs/our-favorite-mac-cleanup-tips.html https://macpaw.com/cleanmymac https://macpaw.com/gemini https://daisydiskapp.com/ https://macpaw.com/cleanmymac newer macOS versions have 'Reduce Clutter' tool https://github.com/docker/for-mac/issues/2297
* file security https://hacker-tools.github.io/security/

prereqs
* [machine compatibility](https://support.apple.com/en-us/HT201475) 
* [space for install](https://blog.macsales.com/45780-get-ready-for-macos-mojave) 
* [run First Aid on startup drive](https://blog.macsales.com/45780-get-ready-for-macos-mojave)
* can't remove standard apps https://apple.stackexchange.com/a/65175/328389

bootable disk https://aaronchall.github.io/#sec-6-2 https://support.apple.com/en-us/HT201372
* disk should be at 16GB
* download OS but don't proceed with install
* grab OS from `Applications`
* https://www.youtube.com/watch?v=Y0NKkOOI9Ew

install from bootable disk
* adjust Energy Saver, plug in power source, `media/video/za` to phone, write down instructions
* insert bootable disk, power on holding `ALT`, folllow video
* troubleshoot https://support.apple.com/en-us/HT201475 + [potential issues](https://blog.macsales.com/45723-mac-installation-errors-you-may-encounter-and-how-to-fix-them)
* load user files

## versions

last time I ran this
```sh
$ defaults write ApplePressAndHoldEnabled -bool f
$ defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false
```
* Apple prevents downloads of older OS versions if you're on Mojave; on other versions, to have access to previous OS you need to have them previously installed and available from the App Store's 'Previously Purchased' tab or find someone who does https://www.macworld.co.uk/how-to/mac-software/download-old-os-x-3629363/#toc-3629363-1
* turn off stacks https://www.tekrevue.com/tip/desktop-files-missing-mojave-stacks/

❌ Big Sur upgrade
* said it need 12gb
* had 18gb
* installed 12gb
* said it needed another 28gb
* I'm out 12gb

✅ Mojave upgrade
* 10.10 to 10.14 bc Sublime and Homebrew started to break and the answer threads looked grim
* caused when I tried to install Vim and it ended up breaking some core libs
* Sublime error -
```sh
# Sublime error https://stackoverflow.com/a/26044247/6813490
plugin_host has exited unexpectedly, plugin functionality wont be available until Sublime Text has been restarted
# Homebrew error https://github.com/Homebrew/homebrew-core/issues/5799
dyld: Library not loaded: /usr/local/opt/readline/lib/libreadline.7.dylib
Referenced from: /usr/local/bin/awk
Reason: image not found
#  Bash/Neofetch error
$ neofetch
dyld: Library not loaded: /usr/local/opt/readline/lib/libreadline.7.dylib
  Referenced from: /usr/local/bin/awk
  Reason: image not found
/usr/local/bin/neofetch: line 4160: 11158 Trace/BPT trap: 5       awk -F'<|>' '/string/ {print $3}' "/System/Library/CoreServices/SystemVersion.plist"
```

# HARDWARE

why
* have a laptop again (work on the couch, Tara's, cafes, parents)
* set up new machine w/ ability to experiment (tmux, neovim)

questions
* music mgmt: sync from Tarsnap?

port
* version mgmt (Python, JS)
* user files @ `~/zvmac`

---


constraints
* Ableton
> is this true anymore? move to analog for now?
* Linux-like
> WSL good enough? not used to Windows keybindings, easier to stick to Mac + their hardware cost competitive

tablet
* notes: Gitlab web IDE
* music production: GarageBand, Koala
* courses from Khan Academy https://github.com/rand-net/khan-dl

## computers

---

| machine   | plus                            | minus                             |
| ----------|---------------------------------|-----------------------------------|
| Mac       | cheap                           | not portable, can't mod           |
| Macbook   | portable                        | can't mod                         |
| Linux     | sysadmin, cheap, easy to mod    | familiarity, hardware, sw support |
| Windows   | duel boot                       | WSL                               |

* Dells break all the time https://news.ycombinator.com/item?id=32632720

specs
* CPU: 
* storage: 
* memory: 16GB is enough https://www.youtube.com/watch?v=SQS7XCgUPmc

Apple
* https://cfenollosa.com/blog/the-m1-macbook-air-one-year-later.html
* ❌ can't upgrade battery or drives since 2015 https://www.youtube.com/watch?v=Q1u2tA9dgCQ
* listings: vendors will list year of OS vs. machine production year, ignore photos (might not even be of the same machine), processor (make sure exact type is listed, that they're quoting base speed, beware if year unlisted) https://www.youtube.com/watch?v=JF1EsYfxwhM
* use 'sold items' to gauge prices https://www.youtube.com/watch?v=b-ltpMVA7BI 6:10
* 2011 unibody: avoid these https://www.youtube.com/watch?v=8jM1brvJhzg 11:45
* 2012 Pro unibody (last pre-retina, easy to add hard drive) https://www.youtube.com/watch?v=8jM1brvJhzg 
* 2014 Air
* 2015 Pro https://www.youtube.com/watch?v=8jM1brvJhzg 3:20

Linux https://www.thinkpenguin.com/
* not ready https://cfenollosa.com/blog/fed-up-with-the-mac-i-spent-six-months-with-a-linux-laptop-the-grass-is-not-greener-on-the-other-side.html
* script install https://blog.jessfraz.com/post/windows-for-linux-nerds/
* lack of support for Ableton, might not have audio interface drivers https://news.ycombinator.com/item?id=20745072
* _Chromebook_: Linux beta https://uglyduck.ca/chromebook-web-development/
* _Dell_: https://cfenollosa.com/blog/fed-up-with-the-mac-i-spent-six-months-with-a-linux-laptop-the-grass-is-not-greener-on-the-other-side.html
* _Framework_: https://frame.work/ https://news.ycombinator.com/item?id=28606962 https://news.ycombinator.com/item?id=27926425
* _System76_: https://system76.com/
* _Thinkpad_: https://news.ycombinator.com/item?id=30241960 x200 https://drewdevault.com/2021/05/14/Pinebook-Pro-review.html beware machines after 2012, X60 can only deal w/ 32-bit os, X200/X220/X230 are popular https://www.youtube.com/watch?v=mxA9Gyyu6Rg 9:45 12:40 13:15

## mbp 2014

🗄 `python-3.10-youtube-ffmpeg.md`

| component    | symptom                                        | cause                                                             |
| -------------|------------------------------------------------|-------------------------------------------------------------------|
| Homebrew     | broken/outdated pkg (newsboat, exa)            | macOS (no Mojave support)                                         |
| pipx         | fixed -> repoint to Homebrew Python 3.10       |                                                                   |
| Python       | fixed -> repoint to Homebrew Python 3.10       | no version mgmt (PSF for 3.6, Homebrew problem = can't get pyenv) |
| macOS        | outdated                                       | no room for Big Sur bc needs 30GB                                 |

| type   | GB (90/120)  | notes                                                         |
|--------|--------------|---------------------------------------------------------------|
| os     | 55           | Library (5GB for app caches, poetry/pip)                      |
| files  | 30           | zvmac, Pictures, Spitfire                                     |
| apps   | 10           | iTerm, Brave, VS-Code, Ableton, flux, VLC, AppCleaner, GitUp  |

* figure out what Mac and availability so if reimage fails you can just go to the mall

---

`system_profiler`
* Model Identifier: MacBookPro11,1
* MacBook Pro (Retina, 13-inch, Mid 2014)
* processor: 2.6 GHz Intel Core i5
* memory: 8 GB 1600 MHz DDR3
* graphics/GPU: Intel Iris 1536 MB
* serial number: C02P2GD4G3QH

about this mac > system report
* Model Name:	MacBook Pro
* Model Identifier:	MacBookPro11,1
* Processor Name:	Intel Core i5
* Processor Speed:	2.6 GHz
* Number of Processors:	1
* Total Number of Cores:	2
* L2 Cache (per Core):	256 KB
* L3 Cache:	3 MB
* Hyper-Threading Technology:	Enabled
* Memory:	8 GB
* Boot ROM Version:	156.0.0.0.0
* SMC Version (system):	2.16f68
* Serial Number (system):	C02P2GD4G3QH
* Hardware UUID:	8297AD35-7359-5F1C-B99F-B8C71A0B4D2B

neofetch

                    'c.          zach@zachs-mbp.lan
                 ,xNMM.          ------------------
               .OMMMMo           OS: macOS Mojave 10.14.6 18G103 x86_64
               OMMM0,            Uptime: 5 days, 9 hours, 22 mins
     .;loddo:' loolloddol;.      Resolution: 1920x1080@2x
   cKMMMMMMMMMMNWMMMMMMMMMM0:    CPU: Intel i5-4278U (4) @ 2.60GHz
 .KMMMMMMMMMMMMMMMMMMMMMMMWd.    Memory: 5001MiB / 8192MiB
 XMMMMMMMMMMMMMMMMMMMMMMMX.      CPU Usage: 11%
;MMMMMMMMMMMMMMMMMMMMMMMM:       Disk (/): 105G / 113G (95%)
:MMMMMMMMMMMMMMMMMMMMMMMM:       Local IP: 192.168.86.33
.MMMMMMMMMMMMMMMMMMMMMMMMX.      Public IP: 76.124.80.235
 kMMMMMMMMMMMMMMMMMMMMMMMMWd.    Packages: 187 (brew)
 .XMMMMMMMMMMMMMMMMMMMMMMMMMMk   Shell: bash 3.2.57
  .XMMMMMMMMMMMMMMMMMMMMMMMMK.   Terminal: iTerm2
    kMMMMMMMMMMMMMMMMMMMMMMd     Terminal Font: FiraMonoNerdFontComplete-Regular 15
     ;KMMMMMMMWXXWMMMMMMMk.
       .cooc,.    .,coo:.

## peripherals

🔍 models https://support.apple.com/en-us/HT201300

monitor
* current: S2318HN/NX Display, 23-inch (1920 x 1080), Intel Iris 1536 MB graphics
* Dell Ultrasharp U3417W; have to wait for newer laptop, resolution no sharper than current monitor when using current laptop
* 1080p vs. 4k https://news.ycombinator.com/item?id=23551983 https://www.youtube.com/watch?v=SQS7XCgUPmc 2:00
* Apple studio display https://www.apple.com/shop/buy-mac/apple-studio-display

KVM
* _KVM switch_: switch keyboard/video/mouse between computers https://www.pcmag.com/how-to/how-to-control-multiple-computers-with-one-keyboard-and-mouse https://www.pcmag.com/picks/best-kvm-switches
> transition: measure space in 2317 (30 mins) swap desks (2 hours) swap desk stands (2 hours)
* ❓ audio
* wiring https://www.youtube.com/watch?v=S9YhQ8e9Q0o
> usb-c/VGA for mbp2022 to monitor https://www.amazon.com/Thunderbolt-Compatible-MacBook-Samsung-Pixelbook/dp/B082R5W86P
> usb-3/usb-c for kvm to mbp2022
```txt
   monitor
    /   \
   |     |
box1     box2
   |     |
    \   /
     KVM
      |
  peripherals
```

---

USB https://en.wikipedia.org/wiki/USB
* _USB_: protocol
* spec is a mess apparently https://news.ycombinator.com/item?id=25724014 https://tidbits.com/2021/12/03/usbefuddled-untangling-the-rats-nest-of-usb-c-standards-and-cables/
* _connector_: hardware for connection e.g. USB-A, micro USB, USB-C
* USB-C https://www.sweetwater.com/insync/what-thunderbolt-3-usb-c-mean-to-musicians/
* _Thunderbolt_: https://www.pcmag.com/news/thunderbolt-3-vs-usb-c-whats-the-difference
* works w/ USB-C https://www.youtube.com/watch?v=H4Z67HfHkN4 6:00

keyboards
* https://www.youtube.com/watch?v=ktMe7azlhic
* chicklet https://www.youtube.com/watch?v=8jM1brvJhzg 5:20 butterfly started with 2015 12' Macbook https://www.theverge.com/2020/5/4/21246223/macbook-keyboard-butterfly-magic-pro-apple-design https://support.apple.com/keyboard-service-program-for-mac-notebooks returned to normal scissor keyboard (aka 'magic') with 2020 16' Macbook Pro https://www.wsj.com/articles/apple-updates-ipad-macbook-air-with-new-keyboard-11584538891
* mechanical keyboard cherry mx browns https://www.keychron.com/ clear is quietest, blue is clicky, brown is chunky https://news.ycombinator.com/item?id=27221191
* _stenography_: = transcription https://www.openstenoproject.org/plover/
* _dead key_: for umlats and tildes

---

* _mouse_: connect external, secondary click
* airpods https://news.ycombinator.com/item?id=30084901
* _battery_: Battery Health 2 https://www.youtube.com/watch?v=UGOJmN3Lc2U 4:30
* _connectors_: used to be magsafe for power, now USB-C https://www.youtube.com/watch?v=8jM1brvJhzg 7:30
* _display_: Retina is Apple's hi-def thing, 'unibody' used to refer to everything that came before https://www.youtube.com/watch?v=8jM1brvJhzg 8:20
* _trackpad_: pretty much the same since 2012 https://www.youtube.com/watch?v=8jM1brvJhzg
* _versions_: can run Mojave (10.14) on anything 2012 and higher https://www.techjunkie.com/macos-mojave-system-requirements/ probably can't run 11 on 2012 Macs https://www.youtube.com/watch?v=8jM1brvJhzg 10:20 https://en.wikipedia.org/wiki/MacOS_version_history#Releases

to watch
* https://www.youtube.com/watch?v=b-ltpMVA7BI @ 6:15
* https://www.youtube.com/watch?v=AmHBOjKlUNY
* https://www.youtube.com/watch?v=EAmoYEYUxlA
* https://www.youtube.com/watch?v=1oykrBFlnY8
* https://www.youtube.com/watch?v=NmVzPufr8pY
* docking station for newer generation Macbooks https://www.youtube.com/watch?v=IGG0sDpqTXA
* _camera_: https://news.ycombinator.com/item?id=23795163
* cleaning https://news.ycombinator.com/item?id=23583611

check on delivery
* check hard drive https://www.youtube.com/watch?v=UGOJmN3Lc2U 5:00
* clean https://www.youtube.com/watch?v=UGOJmN3Lc2U 7:00

## phone

Android
* main: keep, files by google, chrome, calls
* social: whatsapp, messages, gmail, slack, zoom, wechat, contacts, signal
> music mgmt via Android File Transfer on macOS
* music: guitar tuna, pro guitar tuner, perfect ear, liveBPM, Justune https://news.ycombinator.com/item?id=33150260 Koala Sampler https://www.youtube.com/watch?v=Wwq5ChHiGGk musicolet, playtube, music folder player https://play.google.com/store/apps/details?id=de.zorillasoft.musicfolderplayer&hl=en_US&gl=US
* transport: maps, lyft, uber, airbnb, stasher
* language: word reference, easy voice, vlc, libby, overdrive, translate, pleco
* chess/golf: drive, camera, video frame player, chess clock, chess, lichess
* util: clock, interval timer, youtube, play tube, latch, monzo, labcoat, google home, google authenticate

---

* Pine64, Librem, Power, RISC-V ISA https://news.ycombinator.com/item?id=26396582 https://news.ycombinator.com/item?id=30760883
* on not having a phone https://www.alvarez.io/posts/living-like-its99/
* terminal https://holzschu.github.io/a-Shell_iOS/ https://libterm.app/
* _Google Wifi_: nothing dependent on phone, only need email
* _router debug_: turn off and unplug for 5 mins (w/out unplug it doesnn't seem to ever really turn off) get password https://github.com/rauchg/wifi-password

* _requirements_: ❌ two numbers (biz, personal) ✅ overseas ❌ portability from messenger app ❌ OSS
* _Android_: https://kevq.uk/why-im-ditching-android https://www.hexaquo.at/posts/2019/06/29/Freeing+my+phone+from+Google https://eggonomy.com/blogs/news/how-fragmented-is-android normal setting for Messages is 'group MMS', safe mode https://support.google.com/pixelphone/answer/2852139?hl=en bad customer support  https://news.ycombinator.com/item?id=21815260
* _Apple_: ❓ works on Google Fi (incl overseas)?
* _OSS_: https://www.pine64.org/ https://postmarketos.org/ https://www.techrepublic.com/article/librem-5-review-the-linux-based-smartphone-is-not-close-to-consumer-ready
* _dumbphone_: https://news.ycombinator.com/item?id=19423434

apps
* chess: chess.com, lichess
* 交通: lyft, uber, meterUP, google maps
* lang: pleco, translate, audio recording, perfect ear, functional ear trainer, guitar tune
* util: labcoat, monzo, clock, interval timer
* reading: vlc, overdrive, libby, files
* 人脉: wechat, gmail, whatsapp, phone, youtube, msg, signal
* bottom row: chrome, musicolet
* music: koala, smart chord, live bpm, perfect ear, pro guitar tuner, guitar tuna, Vanced https://news.ycombinator.com/item?id=30205848 NewPipe https://newpipe.net/

__WhatsApp__

🔍 艘 'restore chat history following official Change Number guide'

* _premise_: uncoupled to cell number, able to export data
* _irl_: cannot switch number and device simultaneously and preserve chat history, dearth of documentation, WhatsApp customer service will absolutely not help you in any way

[export chat history is broken](https://faq.whatsapp.com/en/android/23756533/) -> this will not necessarily export what you're seeing on your phone, but whatever backup the phone can access i.e. even if you're backup says it was made yesterday, you're account might be reading from something that doesn't include earlier *or* more recent chats. fun right?

* https://stackpointer.io/security/decrypt-whatsapp-crypt8-database-messages/419/
* https://stackpointer.io/security/decrypt-whatsapp-crypt12-database-messages/559/
* https://faq.whatsapp.com/en/android/28000018/?category=5245246
* https://faq.whatsapp.com/en/android/20887921#restore
* https://stackpointer.io/security/decrypt-whatsapp-crypt8-database-messages/419/
* https://stackpointer.io/security/decrypt-whatsapp-crypt12-database-messages/559/

# MACOS

🔍 https://apple.stackexchange.com/

setup
* desktop: enlarge icons (view options)
* dock: rm extas, turn on hiding, turn off 'show recent', pins (terminal, browser)
* silence beep: iTerm (profiles > terminal > notifications > silence bell) http://codingshower.com/how-to-disable-mac-os-annoying-beep-alert-bell-sound-in-terminal-and-iterm2/ global https://apple.stackexchange.com/questions/384025/why-is-my-macbook-pro-beeping-when-performing-a-keyboard-shortcut VS Code https://stackoverflow.com/a/62581536
* enable keyboard repeat/hold: `defaults write -g ApplePressAndHoldEnabled -bool false` (restart apps after setting) https://kingluddite.com/st2/using-vintage-mode-in-sublime-text-the-skinny disabled for 18n https://laceysnr.com/fixing-broken-key-repeat-with-sublime/ https://stackoverflow.com/a/44010683/6813490
* `operation not permitted` -> security > full disk access

za
* `.localized`: i18n e.g. show `/Library` as `/Biblioteca` https://discussions.apple.com/thread/252040
* `scutil`: macOS tool to set hostname, etc.
* disk format: disk utility > select outermost > erase > ExFAT https://www.youtube.com/watch?v=Rq0_PQa8Irs https://www.youtube.com/watch?v=rMkGdnUwvXE
* force quit: `cmd alt esc` or use Activity Monitor (had to kill Docker once this way)
* CLI: https://github.com/rgcr/m-cli settings https://missing.csail.mit.edu/2019/os-customization/

## apps

inventory
* audio: cmus, Sound Source
* macOS: Preview, Pages, Photos
* music: Ableton, Spitfire Audio
* video: VLC, Handbrake
* util: App Cleaner, Disk Drill, Flux, GitUp, Human Japanese, Quicktime

Chrome 🗄 `js.md` browser
* set default browser: system preferences > general
* settings: zoom to 110, font fize large, downloads to desktop, switch search to DuckDuckGo, startup to open previous tabs
* other extensions: Mercury Reader, EditThisCookie, JSON Viewer
* Gmail: have to opt into keyboard shortcuts
* Youtube_: shortcuts `?` skip to % `<num>` list all video titles in playst `youtube-dl --get-filename https://www.youtube.com/playlist?list=PLIiejGE6XOgm_iInCjfVc2Rd0ghl5zJAV > sampling.txt`

Brave
* restore tab: `CMD T`
* reload: `CMD r`
* dev tools: `CMD ALT i`
* bookmarks: `CMD B`

Vimium
* help: `?`
* omnibar: `o`
* tab - search: `T`
* tab - scroll: `J/K`
* nav history: `H/L`
* reload: `r`
* goto input: `gi`
* page - scroll: `j/k`
* page - page: `u/d`
* page - goto: `g/G`
* page - search: `/`
* restore tab: `X`

Spotlight
* access: `CMD SPACE`
* folders to search: apps, calculator, definition, documents, folder, music, pdf documents, system preferences
* NLP = can no longer turn off web search https://forums.macrumors.com/threads/spotlight-how-to-remove-web-search-from-results.2271616/
* alternatives https://news.ycombinator.com/item?id=22849208

Finder
* set default window size: hold CMD when resizing window, then hold ALT and right click Finder in Dock to relaunch https://apple.stackexchange.com/a/192959 
* show file extensions: Finder preferences > advanced
* suppress creation of `DS_Store` seems like a pain https://stackoverflow.com/questions/18015978/how-to-stop-creating-ds-store-on-mac 
* show hidden files: `SHIFT CMD .`
* full list of applications: `about this mac > system report > sw > applications` --> 32-bit apps may not be compatible with macOS 10.14

coloration
* dark mode: set from terminal https://stefan.sofa-rockers.org/2018/10/23/macos-dark-mode-terminal-vim/
* Flux https://justgetflux.com/ https://news.ycombinator.com/item?id=30626803
* NightShift https://shifty.natethompson.io/en/

Preview
* ToC: CMD ALT 3
* higlights: CMD ALT 4
* full screen: CMD SHIFT f
* _views_: cmd <num>
* _goto page_: cmd alt g
* _toggle search_: tab
* _magnify_: ~
* merge: open first PDF, go to last page, `edit > insert > page from file`, use next PDF https://support.apple.com/en-us/HT202945)
* can't close single file when have multiple open https://discussions.apple.com/thread/8135180
* https://news.ycombinator.com/item?id=26681337

VLC 📜 https://wiki.videolan.org/Mac_OS_X/ https://www.maketecheasier.com/mastering-vlc-via-the-command-line-linux/
* _alternatives_: https://iina.io/ https://mpv.io/
* _config_: ❓ is VLC using i.e why isn't long jump 300 seconds (vs 60 seconds) `~/Library/Preferences/org.videolan.vlc/vlcrc` https://superuser.com/a/599305/728972
* _versions_: 3.0.11 (rewind would then play forward but no output audio; macOS version at time 10.14.6) removed and downloaded 3.0.8 and fixed
* help: `--help`
* version: `--version`
* file: `vlc <file>`
* _play/pause_: `SPACE`
* _full screen_: cmd f
* _playback speed up/down_: `CMD =/-`
* _playlist_: cmd alt p
* _jump_: to time (cmd j, then h:m:s) very short () short () mid () long (cmd shift arrow) https://askubuntu.com/a/618391

## dev

processor
* _Rosetta_: gets Intel apps to work on M1 https://news.ycombinator.com/item?id=30799686 https://news.ycombinator.com/item?id=31696447
* iTerm/Terminal > get info > open using Rosetta
```sh
# print architecture
arch
uname -p

# print hardware
uname -m

arch  # i386 w/ Rosetta
arch  # arm64 w/out Rosetta
```

Command Line Tools
* _XCode_: IDE for macOS dev
* _Command Line Tools_: compilers from XCode
* _OSX-GCC installer_: don't install this alongside Command Line Tools https://docs.python-guide.org/starting/install3/osx/
```sh
# install https://apple.stackexchange.com/a/324598
xcode-select --install

# switch
sudo xcode-select --switch /Library/Developer/CommandLineTools

# switch back
sudo xcode-select --reset

# view SDK
xcrun --show-sdk-path

# get fs
xcode-select -p  # /Library/Developer/CommandLineTools

# reintsall
sudo rm -rf $(xcode-select -print-path) # Enter root password. No output is normal.
sudo rm -rf /Library/Developer/CommandLineTools # Enter root password.
sudo xcode-select --reset
xcode-select --install

# update
Warning: A newer Command Line Tools release is available.
Update them from Software Update in System Preferences or run:
  softwareupdate --all --install --force
```

## keybindings

user 
* desktop - show: CMD d; keyboard > shortcuts > mission control
* Chinese: input sources > simplified/pinyin, shortcuts > input sources > select next source in input menu

system
* emoji: CTRL CMD SPACE emoji picker https://matthewpalmer.net/rocket/
* screenshot - whole: CMD SHIFT 3
* screenshot - portion: CMD SHIFT 4
* window - hide: CMD h

symbols
* keyboard viewer https://setapp.com/how-to/type-math-symbols-on-mac
* _copyright_: `alt g`
* _trademark_: `alt 2`
* _delta (∆)_: alt j
* _degree(°)_: alt shift 8
* _infinity_: alt 5
* _accent_: alt e
* _enye_: alt n
* _sigma_: alt w

remap
* keyboard > modifier keys
* common for Vim to do caps lock to esc https://news.ycombinator.com/item?id=24287951
* need to do for each keyboard i.e. built-in, external

---

* _memory usage_: Activity Monitor
* _movie_: CMD SHIFT 5
* _Spanish question mark_: SHIFT ALT ?
* _Spanish exclamation mark_: ALT 1
* [map of macOS key symbols to names](https://www.danrodney.com/mac/)
* _page up/down_ | FN arrows
* _home/end_ | CMD arrows
* _open file_: CMD down arrow
* [function keys](https://support.apple.com/en-us/HT207240): F1 F2 et al.
* [track down large files for cleanup](https://www.youtube.com/watch?v=agtsRgCeAVg)
* _adjust system font size_: system pref - displays - scaled - slider
* _set maximize app_: keyboard - app shortcuts - title shortcut to 'Zoom'

__SQLite extension and `DYLD_LIBRARY_PATH`__

https://forum.djangoproject.com/t/jsonfield-for-sqlite-on-macos-cannot-set-dyld-library-path/3878 https://code.djangoproject.com/ticket/31882#ticket 🗄 `brew/sqlite-dyld.log`

Trying to use `JSONField` with SQLite on macOS [Mojave 10.14]. 
I followed the instructions [here](https://code.djangoproject.com/wiki/JSON1Extension) for how to enable SQLite's `JSON1` extension but was unable to set `DYLD_LIBRARY_PATH` as an environmental variable.
```sh
# attempt to export
$ export DYLD_FALLBACK_LIBRARY_PATH=path/to/dir
# no stdout
$ env | rg DYLD
```
Based on Stack Overflow, inability to set this env var is the result of a [macOS security policy](https://stackoverflow.com/search?q=DYLD_LIBRARY_PATH+macos).
Should the [docs for JSONField using SQLite](https://code.djangoproject.com/wiki/JSON1Extension) be updated? Is there a commonly used workaround to this problem in the Django community?

# MGMT

## photos

* https://news.ycombinator.com/item?id=33046281&utm_term=comment

## music

options
* ❌ headunit: wedded to vehicle, can't rely on this being around much longer https://www.youtube.com/watch?v=AEm2WbSwRIA https://www.amazon.com/KENWOOD-KDC-BT282U-Car-Stereo-Illumination/dp/B09GWC9QYZ models https://www.youtube.com/watch?v=P7pUT0gbZZQ speakers https://www.youtube.com/watch?v=ADFOAAN9SIA
* ❌ home media server: not oriented around file structure
* ✅ Android: enough storage with microSD, good app https://fi.google.com/about/phones/moto-g-5g

---

home media servers
* _Emby_: https://www.youtube.com/watch?v=lgY97D5nCek
* _Jellyfin_: https://www.youtube.com/watch?v=lgY97D5nCek
* _Plex_: 
* _Navidrome_: https://github.com/navidrome/navidrome too expensive to run on cloud https://www.youtube.com/watch?v=RSIvuyLDuvk 2:15
* BYO https://www.youtube.com/watch?v=jf_5FaVFnrU

* text to tree, walk dir https://github.com/birchb1024/frangipanni  https://github.com/BurntSushi/walkdir
* fselect provides useful functionailty for music files 🗄 `shell.md` finder
* BYO tree https://realpython.com/directory-tree-generator-python/

metadata
* music brainz, picard, discogs https://community.metabrainz.org/
* seems like a pain https://bitheap.org/dnuos/ http://oidua.suxbad.com/ https://www.theverge.com/2019/5/29/18531476/music-industry-song-royalties-metadata-credit-problems http://richardmavis.info/tagging-files https://dustri.org/b/horrible-edge-cases-to-consider-when-dealing-with-music.html
* tools: http://beets.io/ + Meta ('Benjamin Jaeger' 🗄 `Applications/Meta`) https://github.com/beetbox/mediafile https://musicbrainz.org/

self-hosted streaming
* _NAS (network attached storage)_: aka 'home media server' 🗄 `network-know-how.pdf`
* aka home server https://www.youtube.com/watch?v=yFuTAKq_j3Q
* options (Plex, cmus remote) https://www.youtube.com/results?search_query=cmus+remote&page=&utm_source=opensearch https://www.youtube.com/watch?v=UJw9YU_SBzo https://blog.dave.tf/post/building-nas-1/ https://www.youtube.com/results?search_query=build+a+nas https://www.youtube.com/results?search_query=buy+a+nas https://kevq.uk/my-home-server-2-months-on/
* https://selfhostedsource.tech/category/self-hosted/audio-streaming
> all this work just to stream music doesn't make sense, just keep rolling w/ backups and your $60 thumb drive
* https://news.ycombinator.com/item?id=30118273

youtube-dl 📜 https://github.com/ytdl-org/youtube-dl 🗄 `python-3.10-youtube-ffmpeg.md`
* alternative https://github.com/soimort/you-get https://news.ycombinator.com/item?id=24904676
* makes Hombrew responsible for ingesting latest version https://github.com/ytdl-org/youtube-dl/issues/20553 
* if 403 run `--rm-cache-dir` https://github.com/ytdl-org/youtube-dl/issues/23638
* _alternatives_: https://github.com/Miserlou/SoundScrape https://git hub.com/Marethyu12/gotube https://github.com/topics/youtube-downloader

pydub
* wrapper over pydub
* https://github.com/jiaaro/pydub https://realpython.com/playing-and-recording-sound-python/
```python
from pydub import AudioSegment
song = AudioSegment.from_mp3("song.mp3")
first_10_seconds = song[:10000]
repeated = first_10_seconds * 2
repeated.export("mashup.mp3", format="mp3")
```

tracking
* poc: `mlib` `os.walk()` https://unix.stackexchange.com/questions/90115/convert-output-of-tree-command-to-json-format/ regex to strip and kebab https://github.com/30-seconds/30-seconds-of-python#kebab https://www.robertchristgau.com/get_gl.php?g=A%2B store library song info as db
```sh
alias mlib="cd /Volumes/MUSIC-LIB && t > ~/Desktop/music-lib-$(date +"%Y%m%d").log"
```
```sh
fd 194[0-9] | wc -l
fd 194[0-9]
fd -t d 194[0-9]
```

# ZA

## Windows

* https://news.ycombinator.com/item?id=25534258
* https://news.ycombinator.com/item?id=22852878
* not MS cares about serving existing customers w/ whatever os it can, not Windows itself https://stratechery.com/2021/intel-problems/
* _remote control_: SSH for Windows
* `-whatif` show results if the command had actually executed!
* _grep_: `dir | find “query”` (quotes required)
* to open a file, just enter full name
* `ls -r`: `dir/s`
* `ls -a`: `Get-ChildItem –Hidden`
* _touch_: `New-Item c:\Users\F618838\Desktop\restOfPath\newFileName.txt -type file`
* copy output to clipboard: `<cmd> | clip`
