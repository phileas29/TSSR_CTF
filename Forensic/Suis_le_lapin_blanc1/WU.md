# WU Suis le lapin blanc 1

## Obtention des informations du profil 


```bash
./volatility_2.6_lin64_standalone -f /home/debian/Téléchargements/lapin_blanc.vmem imageinfo
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win8SP0x64, Win81U1x64, Win2012R2x64_18340, Win2012R2x64, Win2012x64, Win8SP1x64_18340, Win8SP1x64 (Instantiated with Win8SP1x64)
                     AS Layer1 : WindowsAMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/debian/Téléchargements/chall_forensics-Snapshot1.vmem)
                      PAE type : No PAE
                           DTB : 0x1aa000L
                          KDBG : 0xf80144922530L
          Number of Processors : 2
     Image Type (Service Pack) : 0
                KPCR for CPU 0 : 0xfffff8014497f000L
                KPCR for CPU 1 : 0xffffd000bef3c000L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2022-06-24 18:33:05 UTC+0000
     Image local date and time : 2022-06-24 20:33:05 +0200
```

## Obtention des informations de ruches du registre

Après plusieurs tentatives de profils de volatility on obtient finalement un résultat avec le profil Win8SP1x64_18340

```bash
./volatility_2.6_lin64_standalone -f /home/debian/Téléchargements/lapin_blanc.vmem --profile=Win8SP1x64_18340 hivelist
Volatility Foundation Volatility Framework 2.6
Virtual            Physical           Name
------------------ ------------------ ----
0xffffc0004a898000 0x00000000046c2000 \SystemRoot\System32\Config\DEFAULT
0xffffc00047626000 0x00000000318b0000 \SystemRoot\System32\Config\SECURITY
0xffffc0004767c000 0x000000002b72c000 \SystemRoot\System32\Config\SAM
0xffffc0004772c000 0x000000002bd05000 \??\C:\Windows\ServiceProfiles\NetworkService\NTUSER.DAT
0xffffc000477ac000 0x000000002c36f000 \SystemRoot\System32\Config\BBI
0xffffc0004e5b5000 0x0000000032406000 \??\C:\Windows\ServiceProfiles\LocalService\NTUSER.DAT
0xffffc00047aeb000 0x00000000014ce000 \??\C:\Users\Neo\ntuser.dat
0xffffc00048211000 0x000000006fe66000 \??\C:\Users\Neo\AppData\Local\Microsoft\Windows\UsrClass.dat
0xffffc00048fb6000 0x0000000063ca4000 \SystemRoot\System32\config\DRIVERS
0xffffc0004ed2e000 0x0000000019c7c000 \??\C:\Windows\AppCompat\Programs\Amcache.hve
0xffffc00046c1f000 0x00000000001e7000 [no name]
0xffffc00046c28000 0x00000000001f1000 \REGISTRY\MACHINE\SYSTEM
0xffffc00046c50000 0x000000000014e000 \REGISTRY\MACHINE\HARDWARE
0xffffc00047016000 0x000000002af45000 \Device\HarddiskVolume1\Boot\BCD
0xffffc0004755d000 0x0000000079b1a000 \SystemRoot\System32\Config\SOFTWARE
```

### Trouver le nom de la machine

La ruche \REGISTRY\MACHINE\SYSTEM nous intéresse, on affiche son contenu en se servant de son adresse mémoire virtuelle : 0xffffc00046c28000

```bash
./volatility_2.6_lin64_standalone -f /home/debian/Téléchargements/lapin_blanc.vmem --profile=Win8SP1x64_18340 printkey -o 0xffffc00046c28000
Volatility Foundation Volatility Framework 2.6
Legend: (S) = Stable   (V) = Volatile

----------------------------
Registry: \REGISTRY\MACHINE\SYSTEM
Key name: CsiTool-CreateHive-{00000000-0000-0000-0000-000000000000} (S)
Last updated: 2022-06-24 18:27:27 UTC+0000

Subkeys:
  (S) ControlSet001
  (S) DriverDatabase
  (S) HardwareConfig
  (S) MountedDevices
  (S) RNG
  (S) Select
  (S) Setup
  (S) WPA
  (V) CurrentControlSet
```

En connaissant l'architecture des ruches du registe Windows, on sait qu'on peut trouver le nom de la machine dans HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\ComputerName\ComputerName

On continue dans la recherche en précisant les sous-clés :

```bash
./volatility_2.6_lin64_standalone -f /home/debian/Téléchargements/lapin_blanc.vmem --profile=Win8SP1x64_18340 printkey -o 0xffffc00046c28000 -K "ControlSet001\Control\ComputerName\ComputerName"
Volatility Foundation Volatility Framework 2.6
Legend: (S) = Stable   (V) = Volatile

----------------------------
Registry: \REGISTRY\MACHINE\SYSTEM
Key name: ComputerName (S)
Last updated: 2022-06-24 18:27:16 UTC+0000

Subkeys:

Values:
REG_SZ                        : (S) mnmsrvc
REG_SZ        ComputerName    : (S) ENTERTHEMATRIX
```

Le flag est donc TSSR{ENTERTHEMATRIX}
