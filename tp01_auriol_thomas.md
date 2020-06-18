# TP 1 Maîtrise de poste
## Self-footprinting
### Host OS

- **nom de la machine :**
> `(gwmi win32_operatingsystem).CSName`
> DESKTOP-HLFJNKP
- **OS et version :**
> `(gwmi win32_operatingsystem).name`
> Microsoft Windows 10 Professionnel
- **architecture processeur (32-bit, 64-bit, ARM, etc) :**
> `(gwmi win32_operatingsystem).OSArchitecture`
> 64 bits
- **modèle du processeur :**
> `(gwmi win32_Processor).name`
> Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz
- **quantité RAM et modèle de la RAM :**
> `gwmi win32_physicalmemory | Format-Table Manufacturer,Banklabel,Configuredclockspeed,Capacity -autosize`
> ```
> Manufacturer Banklabel Configuredclockspeed    Capacity
> ------------ --------- --------------------    --------
> 029E         BANK 0                    2667 17179869184
> 029E         BANK 2                    2667 17179869184
> ```

### Devices

-  **Marque, modèle du processeur, nombre de processeurs et nombre de coeur :**
> `Get-WmiObject Win32_Processor | Format-Table Manufacturer,deivceid,name,numberofcores,numberoflogicalprocessors`
> ```
> Manufacturer deviceid name                                     numberofcores numberoflogicalprocessors
> ------------ -------- ----                                     ------------- -------------------------
> GenuineIntel CPU0     Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz             6                        12
> ```

Le nom de mon processeur est constitué de plusieurs élément, Intel(R) Core(TM) est le nom de la marque, i7 correspond à sa gamme de produit, le 9 est la génération du processeur, le 750 correspond au numéro de référence (SKU) et le H signifie Graphiques hautes performances.



-- **Marque et modèle** :
- **Touchpad / Trackpad** : 
> `Get-PnpDevice -Class "HIDClass"`
> ```
> Status     Class           FriendlyName
> ------     -----           ------------
> OK         HIDClass        Clavier tactile compatible HID
> ```
- **Enceintes intégrées** : 
> `Get-PnpDevice -Class "AudioEndpoint"`
> ```
> Status     Class           FriendlyName
> ------     -----           ------------
> OK         AudioEndpoint   Speakers (Realtek(R) Audio)
> ```
- **Disque dur principal** : 
> `Get-PhysicalDisk`
> ```
> Number FriendlyName            SerialNumber                             MediaType CanPool OperationalStatus HealthStatus Usage            Size
> ------ ------------            ------------                             --------- ------- ----------------- ------------ -----            ----
> 1      WDS500G3X0C-00SJG0      1909_9A80_2470_0001_001B_448B_44BB_7F68. SSD       False   OK                Healthy      Auto-Select 465.76 GB
> ```

-- **Disque dur :**
- **Partitions et système de fichier :**
>`Get-Partition`
>```
>DiskPath : \\?\scsi#disk&ven_nvme&prod_wds500g3x0c-00sj#5&19f9da17&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}
>
>PartitionNumber  DriveLetter Offset                                        Size Type
>---------------  ----------- ------                                        ---- ----
>1                            1048576                                     260 MB System
>2                            273678336                                   128 MB Reserved
>3                            407896064                                   500 MB Recovery
>4                C           932184064                                464.89 GB Basic
>
>DiskPath : \\?\scsi#disk&ven_samsung&prod_ssd_860_qvo_1tb#4&2ebbb2e4&0&000000#{53f56307-b6bf-11d0-94f2-00a0c91efb8b}
>
>PartitionNumber  DriveLetter Offset                                        Size Type
>---------------  ----------- ------                                        ---- ----
>1                            17408                                     15.98 MB Reserved
>2                D           16777216                                  931.5 GB Basic
>```

### Network

-- **Afficher la liste des cartes réseau de votre machine :**
>`Get-NetAdapter | Format-Table Name, InterfaceDescription`
>```
>Name                            InterfaceDescription
>----                            --------------------
>VirtualBox Host-Only Network #4 VirtualBox Host-Only Ethernet Adapter #4
>VirtualBox Host-Only Network #2 VirtualBox Host-Only Ethernet Adapter #2
>VirtualBox Host-Only Network #3 VirtualBox Host-Only Ethernet Adapter #3
>Wi-Fi                           Killer(R) Wireless-AC 1550 Wireless Network Adapter (9260NGW) 160MHz
>VirtualBox Host-Only Network    VirtualBox Host-Only Ethernet Adapter
>VirtualBox Host-Only Network #5 VirtualBox Host-Only Ethernet Adapter #5
>Ethernet                        Realtek PCIe GBE Family Controller
>```
- Wifi: Carte Wifi
- Ethernet: Carte ethernet
- Virtualbox: Carte virtuel de virtualbox
- Bluetooth: Permet l'accés au bluetooth (désactivé au moment de la commande)

-- **Lister tous les ports TCP et UDP en utilisation :**
>`netstat -ano`
>```
>Connexions actives
>
>  Proto  Adresse locale         Adresse distante       État
>  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       1264
>  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
>  TCP    0.0.0.0:5040           0.0.0.0:0              LISTENING       9000
>  TCP    0.0.0.0:7680           0.0.0.0:0              LISTENING       12180
>  TCP    0.0.0.0:49664          0.0.0.0:0              LISTENING       656
>  TCP    0.0.0.0:49665          0.0.0.0:0              LISTENING       8
>  TCP    0.0.0.0:49666          0.0.0.0:0              LISTENING       564
>  TCP    0.0.0.0:49667          0.0.0.0:0              LISTENING       2828
>  TCP    0.0.0.0:49668          0.0.0.0:0              LISTENING       3400
>  TCP    0.0.0.0:49669          0.0.0.0:0              LISTENING       4216
>  TCP    0.0.0.0:49670          0.0.0.0:0              LISTENING       568
>  TCP    10.2.1.1:139           0.0.0.0:0              LISTENING       4
>  TCP    10.3.1.1:139           0.0.0.0:0              LISTENING       4
>  TCP    10.3.2.1:139           0.0.0.0:0              LISTENING       4
>  TCP    127.0.0.1:1641         127.0.0.1:65001        ESTABLISHED     4788
>  TCP    127.0.0.1:1686         0.0.0.0:0              LISTENING       17992
>  TCP    127.0.0.1:1686         127.0.0.1:1702         ESTABLISHED     17992
>  TCP    127.0.0.1:1702         127.0.0.1:1686         ESTABLISHED     25792
>  TCP    127.0.0.1:1790         0.0.0.0:0              LISTENING       12956
> TCP    127.0.0.1:1936         127.0.0.1:11456        ESTABLISHED     23224
>  TCP    127.0.0.1:2481         0.0.0.0:0              LISTENING       17224
>  TCP    127.0.0.1:2488         0.0.0.0:0              LISTENING       17224
>  TCP    127.0.0.1:4907         0.0.0.0:0              LISTENING       17224
>  TCP    127.0.0.1:6463         0.0.0.0:0              LISTENING       23280
>  TCP    127.0.0.1:11456        0.0.0.0:0              LISTENING       5940
>  TCP    127.0.0.1:11456        127.0.0.1:1936         ESTABLISHED     5940
>  TCP    127.0.0.1:15292        0.0.0.0:0              LISTENING       23748
>  TCP    127.0.0.1:15393        0.0.0.0:0              LISTENING       23748
>  TCP    127.0.0.1:16494        0.0.0.0:0              LISTENING       23748
>  TCP    127.0.0.1:45623        0.0.0.0:0              LISTENING       17224
>  TCP    127.0.0.1:65001        0.0.0.0:0              LISTENING       4788
>  TCP    127.0.0.1:65001        127.0.0.1:1641         ESTABLISHED     4788
>  TCP    192.168.43.60:139      0.0.0.0:0              LISTENING       4
>  TCP    192.168.43.60:1680     172.217.18.206:443     CLOSE_WAIT      3776
>  TCP    192.168.43.60:1708     172.217.18.206:443     CLOSE_WAIT      25844
>  TCP    192.168.43.60:1736     23.57.5.23:443         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1737     93.184.220.29:80       CLOSE_WAIT      8416
>  TCP    192.168.43.60:1738     23.57.5.23:443         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1740     23.57.5.23:443         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1741     23.57.5.23:443         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1743     23.57.6.200:80         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1746     23.57.6.200:80         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1747     23.57.6.200:80         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1748     23.57.6.200:80         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1749     23.57.6.200:80         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1750     23.57.6.200:80         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1751     23.57.6.200:80         CLOSE_WAIT      8416
>  TCP    192.168.43.60:1755     23.57.5.23:443         CLOSE_WAIT      8416
>  TCP    192.168.43.60:2877     23.57.6.117:443        CLOSE_WAIT      816
>  TCP    192.168.43.60:4590     40.67.251.132:443      ESTABLISHED     4736
>  TCP    192.168.43.60:4617     66.102.1.188:5228      ESTABLISHED     23224
>  TCP    192.168.43.60:5600     162.159.128.235:443    ESTABLISHED     17900
>  TCP    192.168.43.60:5602     162.159.138.234:443    ESTABLISHED     17900
>  TCP    192.168.43.60:5603     104.20.52.28:443       ESTABLISHED     23664
>  TCP    192.168.43.60:5604     34.252.34.56:443       ESTABLISHED     1700
>  TCP    192.168.43.60:5742     54.64.181.150:443      ESTABLISHED     23224
>  TCP    192.168.43.60:5766     140.82.112.25:443      ESTABLISHED     23224
>  TCP    192.168.43.60:5822     34.232.250.4:443       ESTABLISHED     1700
>  TCP    192.168.43.60:5826     162.159.130.233:443    ESTABLISHED     17900
>  TCP    192.168.43.60:5827     162.159.136.234:443    ESTABLISHED     17900
>  TCP    192.168.43.60:5843     151.101.2.49:443       ESTABLISHED     23224
>  TCP    192.168.43.60:5847     18.179.179.211:443     ESTABLISHED     23224
>  TCP    192.168.43.60:5858     172.217.18.195:443     ESTABLISHED     23224
>  TCP    192.168.43.60:5861     40.67.188.15:443       ESTABLISHED     35012
>  TCP    192.168.43.60:5862     52.157.234.37:443      ESTABLISHED     20900
>  TCP    192.168.56.1:139       0.0.0.0:0              LISTENING       4
>  TCP    192.168.240.1:139      0.0.0.0:0              LISTENING       4
>  TCP    [::]:135               [::]:0                 LISTENING       1264
>  TCP    [::]:445               [::]:0                 LISTENING       4
>  TCP    [::]:7680              [::]:0                 LISTENING       12180
>  TCP    [::]:49664             [::]:0                 LISTENING       656
>  TCP    [::]:49665             [::]:0                 LISTENING       8
>  TCP    [::]:49666             [::]:0                 LISTENING       564
>  TCP    [::]:49667             [::]:0                 LISTENING       2828
>  TCP    [::]:49668             [::]:0                 LISTENING       3400
>  TCP    [::]:49669             [::]:0                 LISTENING       4216
>  TCP    [::]:49670             [::]:0                 LISTENING       568
>  UDP    0.0.0.0:500            *:*                                    4976
>  UDP    0.0.0.0:4500           *:*                                    4976
>  UDP    0.0.0.0:5050           *:*                                    9000
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    2836
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
>  UDP    0.0.0.0:5353           *:*                                    29500
> UDP    0.0.0.0:5353           *:*                                    23224
>  UDP    0.0.0.0:5355           *:*                                    2836
>  UDP    0.0.0.0:55288          *:*                                    23280
>  UDP    0.0.0.0:57615          *:*                                    23280
>  UDP    0.0.0.0:62763          *:*                                    23224
>  UDP    0.0.0.0:64858          *:*                                    4788
>  UDP    10.2.1.1:137           *:*                                    4
>  UDP    10.2.1.1:138           *:*                                    4
>  UDP    10.2.1.1:1900          *:*                                    4036
>  UDP    10.2.1.1:2177          *:*                                    3696
>  UDP    10.2.1.1:5353          *:*                                    4788
>  UDP    10.2.1.1:65001         *:*                                    4036
>  UDP    10.3.1.1:137           *:*                                    4
>  UDP    10.3.1.1:138           *:*                                    4
>  UDP    10.3.1.1:1900          *:*                                    4036
>  UDP    10.3.1.1:2177          *:*                                    3696
>  UDP    10.3.1.1:5353          *:*                                    4788
>  UDP    10.3.1.1:65003         *:*                                    4036
>  UDP    10.3.2.1:137           *:*                                    4
>  UDP    10.3.2.1:138           *:*                                    4
>  UDP    10.3.2.1:1900          *:*                                    4036
> UDP    10.3.2.1:2177          *:*                                    3696
>  UDP    10.3.2.1:5353          *:*                                    4788
>  UDP    10.3.2.1:65004         *:*                                    4036
> UDP    127.0.0.1:1900         *:*                                    4036
>  UDP    127.0.0.1:10030        *:*                                    17992
>  UDP    127.0.0.1:50891        *:*                                    11760
> UDP    127.0.0.1:52019        *:*                                    4708
>  UDP    127.0.0.1:65006        *:*                                    4036
>  UDP    192.168.43.60:137      *:*                                    4
>  UDP    192.168.43.60:138      *:*                                    4
>  UDP    192.168.43.60:1900     *:*                                    4036
>  UDP    192.168.43.60:2177     *:*                                    3696
>  UDP    192.168.43.60:5353     *:*                                    4788
>  UDP    192.168.43.60:65005    *:*                                    4036
>  UDP    192.168.56.1:137       *:*                                    4
>  UDP    192.168.56.1:138       *:*                                    4
>  UDP    192.168.56.1:1900      *:*                                    4036
>  UDP    192.168.56.1:2177      *:*                                    3696
>  UDP    192.168.56.1:5353      *:*                                    4788
>  UDP    192.168.56.1:65000     *:*                                    4036
>  UDP    192.168.240.1:137      *:*                                    4
>  UDP    192.168.240.1:138      *:*                                    4
>  UDP    192.168.240.1:1900     *:*                                    4036
>  UDP    192.168.240.1:2177     *:*                                    3696
>  UDP    192.168.240.1:5353     *:*                                    4788
>  UDP    192.168.240.1:65002    *:*                                    4036
>  UDP    [::]:500               *:*                                    4976
>  UDP    [::]:4500              *:*                                    4976
>  UDP    [::]:5353              *:*                                    2836
>  UDP    [::]:5353              *:*                                    29500
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5353              *:*                                    29500
>  UDP    [::]:5353              *:*                                    29500
>  UDP    [::]:5353              *:*                                    29500
>  UDP    [::]:5353              *:*                                    29500
>  UDP    [::]:5353              *:*                                    29500
>  UDP    [::]:5353              *:*                                    23224
>  UDP    [::]:5355              *:*                                    2836
>  UDP    [::]:64859             *:*                                    4788
>  UDP    [::1]:1900             *:*                                    4036
>  UDP    [::1]:5353             *:*                                    4788
>  UDP    [::1]:52032            *:*                                    5632
>  UDP    [::1]:52033            *:*                                    5632
>  UDP    [::1]:64999            *:*                                    4036
>  UDP    [fe80::952:ff73:ee4f:4912%16]:1900  *:*                                    4036
>  UDP    [fe80::952:ff73:ee4f:4912%16]:2177  *:*                                    3696
>  UDP    [fe80::952:ff73:ee4f:4912%16]:64993  *:*                                    4036
>  UDP    [fe80::cdc:b517:a276:f801%20]:1900  *:*                                    4036
>  UDP    [fe80::cdc:b517:a276:f801%20]:2177  *:*                                    3696
>  UDP    [fe80::cdc:b517:a276:f801%20]:64995  *:*                                    4036
>  UDP    [fe80::1df4:886e:b574:f28c%18]:1900  *:*                                    4036
>  UDP    [fe80::1df4:886e:b574:f28c%18]:2177  *:*                                    3696
>  UDP    [fe80::1df4:886e:b574:f28c%18]:64998  *:*                                    4036
>  UDP    [fe80::780c:79fb:53bc:d219%12]:1900  *:*                                    4036
>  UDP    [fe80::780c:79fb:53bc:d219%12]:2177  *:*                                    3696
>  UDP    [fe80::780c:79fb:53bc:d219%12]:64997  *:*                                    4036
>  UDP    [fe80::7d49:dcca:c033:b107%21]:1900  *:*                                    4036
> UDP    [fe80::7d49:dcca:c033:b107%21]:2177  *:*                                    3696
>  UDP    [fe80::7d49:dcca:c033:b107%21]:64994  *:*                                    4036
>  UDP    [fe80::9533:1cb5:2d0a:3c4e%23]:1900  *:*                                    4036
>  UDP    [fe80::9533:1cb5:2d0a:3c4e%23]:2177  *:*                                    3696
>  UDP    [fe80::9533:1cb5:2d0a:3c4e%23]:64996  *:*                                    4036
>```

- **déterminer quel programme tourne derrière chacun des ports :**
>`Get-Process | Where-Object {$_.mainWindowTitle} | Format-Table Id, Name, mainWindowtitle`
>```
>   Id Name                                                           MainWindowTitle
>   -- ----                                                           ---------------
> 6560 ApplicationFrameHost                                           Paramètres
> 1952 Discord                                                        📝 Cour 9 - Discord
>27128 HxOutlook                                                      Courrier
>25792 NVIDIA Share                                                   NVIDIA GeForce Overlay
>35700 powershell                                                     Windows PowerShell
> 9336 SystemSettings                                                 Paramètres
>17744 WindowsInternal.ComposableShell.Experiences.TextInput.InputApp Microsoft Text Input Application
> 8416 WinStore.App                                                   Microsoft Store
>```

### Users

-- **Déterminer la liste des utilisateurs de la machine :**
>`Get-LocalUser`
>```
>Name               Enabled Description
>----               ------- -----------
>Administrateur     False   Compte d’utilisateur d’administration
>DefaultAccount     False   Compte utilisateur géré par le système.
>Invité             False   Compte d’utilisateur invité
>tauri              True
>WDAGUtilityAccount False   Compte d’utilisateur géré et utilisé par le système pour les scénarios Windows Defender Application Guard.
>```

- **déterminer le nom de l'utilisateur qui est full admin sur la machin :**
> Administrateur

### Processus
-- **Déterminer la liste des processus de la machine :**
>`tasklist`
>```
>Nom de l’image                 PID Nom de la sessio Numéro de s Utilisation
>========================= ======== ================ =========== ============
>System Idle Process              0 Services                   0         8 Ko
>System                           4 Services                   0     3,592 Ko
>Registry                       144 Services                   0    38,732 Ko
>smss.exe                       612 Services                   0       388 Ko
>csrss.exe                      768 Services                   0     2,288 Ko
>wininit.exe                      8 Services                   0     1,844 Ko
>services.exe                   568 Services                   0     7,872 Ko
>lsass.exe                      656 Services                   0    15,936 Ko
>svchost.exe                    672 Services                   0     1,212 Ko
>svchost.exe                   1040 Services                   0    25,908 Ko
>fontdrvhost.exe               1064 Services                   0     1,748 Ko
>WUDFHost.exe                  1072 Services                   0     2,156 Ko
>svchost.exe                   1264 Services                   0    14,604 Ko
>svchost.exe                   1336 Services                   0     5,548 Ko
>svchost.exe                   1504 Services                   0     5,148 Ko
>svchost.exe                   1536 Services                   0     2,948 Ko
>svchost.exe                   1544 Services                   0     4,716 Ko
>svchost.exe                   1552 Services                   0     3,376 Ko
>svchost.exe                   1744 Services                   0     5,828 Ko
>svchost.exe                   1752 Services                   0     4,856 Ko
>svchost.exe                   1868 Services                   0     2,504 Ko
>svchost.exe                   1888 Services                   0     2,216 Ko
>svchost.exe                   1896 Services                   0     4,324 Ko
>svchost.exe                   2024 Services                   0     3,184 Ko
>svchost.exe                   2044 Services                   0     3,688 Ko
>svchost.exe                    564 Services                   0    13,240 Ko
>svchost.exe                   2144 Services                   0     4,844 Ko
>svchost.exe                   2260 Services                   0     2,072 Ko
>igfxCUIService.exe            2296 Services                   0     2,628 Ko
>svchost.exe                   2308 Services                   0     9,528 Ko
>svchost.exe                   2316 Services                   0    37,700 Ko
>svchost.exe                   2324 Services                   0     2,056 Ko
>NVDisplay.Container.exe       2432 Services                   0     7,640 Ko
>svchost.exe                   2456 Services                   0     4,500 Ko
>svchost.exe                   2528 Services                   0     6,644 Ko
>dasHost.exe                   2636 Services                   0     1,556 Ko
>svchost.exe                   2648 Services                   0     5,608 Ko
>svchost.exe                   2784 Services                   0    14,616 Ko
>svchost.exe                   2796 Services                   0     9,660 Ko
>svchost.exe                   2828 Services                   0     9,800 Ko
>svchost.exe                   2836 Services                   0     5,428 Ko
>svchost.exe                   2932 Services                   0     2,468 Ko
>svchost.exe                   2960 Services                   0     1,736 Ko
>svchost.exe                   2968 Services                   0     6,528 Ko
>svchost.exe                   2400 Services                   0     4,248 Ko
>svchost.exe                   2464 Services                   0     4,956 Ko
>Memory Compression            2780 Services                   0     6,804 Ko
>svchost.exe                   3112 Services                   0     6,636 Ko
>svchost.exe                   3156 Services                   0     3,140 Ko
>svchost.exe                   3400 Services                   0     2,864 Ko
>svchost.exe                   3436 Services                   0    14,188 Ko
>svchost.exe                   3516 Services                   0     3,976 Ko
>svchost.exe                   3844 Services                   0     9,440 Ko
>svchost.exe                   4000 Services                   0     5,840 Ko
>svchost.exe                   4008 Services                   0     2,976 Ko
>svchost.exe                   3660 Services                   0    12,164 Ko
>svchost.exe                   4036 Services                   0     3,908 Ko
>svchost.exe                   4148 Services                   0     3,944 Ko
>spoolsv.exe                   4216 Services                   0     9,944 Ko
>wlanext.exe                   4228 Services                   0     1,824 Ko
>conhost.exe                   4240 Services                   0     6,624 Ko
>svchost.exe                   4324 Services                   0    17,960 Ko
>svchost.exe                   4680 Services                   0    32,940 Ko
>svchost.exe                   4696 Services                   0     9,856 Ko
>svchost.exe                   4708 Services                   0     8,300 Ko
>ibtsiva.exe                   4716 Services                   0       836 Ko
>svchost.exe                   4736 Services                   0    13,924 Ko
>svchost.exe                   4744 Services                   0     2,600 Ko
>svchost.exe                   4752 Services                   0     1,900 Ko
>svchost.exe                   4764 Services                   0     1,184 Ko
>WTabletServicePro.exe         4772 Services                   0    11,896 Ko
>IntelCpHDCPSvc.exe            4780 Services                   0     2,200 Ko
>nvcontainer.exe               4788 Services                   0    19,972 Ko
>Creative.UWPRPCService.ex     4796 Services                   0     1,392 Ko
>MsMpEng.exe                   4820 Services                   0   974,176 Ko
>svchost.exe                   4896 Services                   0    48,132 Ko
>svchost.exe                   4936 Services                   0     2,536 Ko
>svchost.exe                   4976 Services                   0     3,472 Ko
>IntelCpHeciSvc.exe            5252 Services                   0     2,020 Ko
>svchost.exe                   5344 Services                   0     3,952 Ko
>svchost.exe                   5376 Services                   0     1,460 Ko
>KillerNetworkService.exe      5396 Services                   0   126,716 Ko
>svchost.exe                   5632 Services                   0    10,368 Ko
>svchost.exe                   6208 Services                   0     4,072 Ko
>svchost.exe                   6932 Services                   0     2,236 Ko
>dllhost.exe                   4612 Services                   0     6,440 Ko
>svchost.exe                   7108 Services                   0     4,356 Ko
>NisSrv.exe                    2420 Services                   0     9,932 Ko
>svchost.exe                   7400 Services                   0     2,492 Ko
>svchost.exe                   7624 Services                   0     5,552 Ko
>svchost.exe                   7584 Services                   0     6,344 Ko
>dllhost.exe                   7568 Services                   0     5,800 Ko
>PresentationFontCache.exe     6120 Services                   0     8,392 Ko
>svchost.exe                   8544 Services                   0    11,820 Ko
>svchost.exe                   9000 Services                   0    11,168 Ko
>svchost.exe                  10456 Services                   0    11,476 Ko
>svchost.exe                  11072 Services                   0     7,996 Ko
>svchost.exe                  11936 Services                   0    14,256 Ko
>GoogleCrashHandler.exe       12248 Services                   0     1,124 Ko
>GoogleCrashHandler64.exe      7060 Services                   0     1,004 Ko
>SecurityHealthService.exe    13052 Services                   0     8,888 Ko
>svchost.exe                   5544 Services                   0     5,784 Ko
>svchost.exe                   3696 Services                   0     4,724 Ko
>svchost.exe                  14736 Services                   0     1,876 Ko
>svchost.exe                  12180 Services                   0    12,664 Ko
>svchost.exe                   6636 Services                   0     6,244 Ko
>SgrmBroker.exe               15488 Services                   0     4,816 Ko
>svchost.exe                  15572 Services                   0     4,044 Ko
>svchost.exe                   7104 Services                   0     3,256 Ko
>svchost.exe                  11368 Services                   0     4,148 Ko
>svchost.exe                   5204 Services                   0     2,080 Ko
>OfficeClickToRun.exe         26528 Services                   0    58,100 Ko
>AppVShNotify.exe             28848 Services                   0     1,984 Ko
>SearchIndexer.exe            10236 Services                   0    49,628 Ko
>svchost.exe                  28644 Services                   0     3,168 Ko
>csrss.exe                    16556 Console                    3     3,736 Ko
>winlogon.exe                 15664 Console                    3     3,920 Ko
>fontdrvhost.exe              30392 Console                    3     9,776 Ko
>dwm.exe                      28632 Console                    3   279,600 Ko
>NVDisplay.Container.exe      13380 Console                    3    45,252 Ko
>svchost.exe                  33132 Services                   0     1,500 Ko
>nvcontainer.exe               3936 Console                    3     7,824 Ko
>sihost.exe                   24648 Console                    3    26,488 Ko
>nvcontainer.exe              11760 Console                    3    48,424 Ko
>svchost.exe                  20900 Console                    3    20,940 Ko
>igfxEM.exe                   12192 Console                    3    19,196 Ko
>svchost.exe                  21036 Console                    3    31,396 Ko
>ipoint.exe                   17220 Console                    3     2,640 Ko
>itype.exe                    18552 Console                    3     2,556 Ko
>taskhostw.exe                12468 Console                    3    15,040 Ko
>explorer.exe                  9452 Console                    3   186,552 Ko
>svchost.exe                  30280 Console                    3    16,356 Ko
>StartMenuExperienceHost.e    11604 Console                    3    50,712 Ko
>RuntimeBroker.exe            26452 Console                    3     5,476 Ko
>SearchUI.exe                 22812 Console                    3   190,640 Ko
>ctfmon.exe                   29004 Console                    3    10,032 Ko
>RuntimeBroker.exe             9876 Console                    3    35,592 Ko
>YourPhone.exe                31780 Console                    3     9,796 Ko
>SettingSyncHost.exe           7228 Console                    3     4,176 Ko
>NVIDIA Web Helper.exe        17992 Console                    3    10,324 Ko
>TabTip.exe                   19228 Console                    3     8,648 Ko
>LockApp.exe                   2708 Console                    3    11,108 Ko
>RuntimeBroker.exe            31988 Console                    3    20,048 Ko
>MKCHelper.exe                17120 Console                    3     1,052 Ko
>RuntimeBroker.exe            15188 Console                    3    10,984 Ko
>RuntimeBroker.exe            26212 Console                    3     6,276 Ko
>Wacom_TabletUser.exe          2628 Console                    3     3,612 Ko
>WacomHost.exe                29440 Console                    3     2,416 Ko
>conhost.exe                   5984 Console                    3     1,080 Ko
>Wacom_Tablet.exe              3776 Console                    3    16,936 Ko
>Wacom_TouchUser.exe          25844 Console                    3     8,336 Ko
>svchost.exe                  16476 Console                    3    16,760 Ko
>nvsphelper64.exe             32384 Console                    3     4,376 Ko
>NVIDIA Share.exe             25792 Console                    3    24,208 Ko
>NVIDIA Share.exe              9600 Console                    3    20,520 Ko
>NVIDIA Share.exe             23756 Console                    3    65,368 Ko
>SecurityHealthSystray.exe     2912 Console                    3     2,592 Ko
>Discord.exe                   1952 Console                    3    64,064 Ko
>Discord.exe                  30172 Console                    3   177,528 Ko
>Discord.exe                  17900 Console                    3    19,760 Ko
>IGCCTray.exe                 12100 Console                    3    24,628 Ko
>Discord.exe                  31616 Console                    3     5,488 Ko
>Discord.exe                  23280 Console                    3   506,216 Ko
>IGCC.exe                     23952 Console                    3    17,600 Ko
>Discord.exe                  26752 Console                    3     9,680 Ko
>ApplicationFrameHost.exe      6560 Console                    3    30,216 Ko
>WinStore.App.exe              8416 Console                    3    44,992 Ko
>RuntimeBroker.exe            33364 Console                    3    10,348 Ko
>RuntimeBroker.exe            12988 Console                    3     7,448 Ko
>HxOutlook.exe                27128 Console                    3       488 Ko
>HxTsr.exe                    27396 Console                    3    15,560 Ko
>Microsoft.Photos.exe         20052 Console                    3    44,600 Ko
>RuntimeBroker.exe            24688 Console                    3    25,132 Ko
>Dashlane.exe                 12956 Console                    3    35,936 Ko
>CompPkgSrv.exe                7672 Console                    3     4,548 Ko
>rundll32.exe                 17088 Console                    3     4,308 Ko
>DashlanePlugin.exe            5940 Console                    3    45,448 Ko
>svchost.exe                  15756 Console                    3     2,340 Ko
>chrome.exe                   29500 Console                    3   209,456 Ko
>chrome.exe                   31408 Console                    3     2,944 Ko
>chrome.exe                   27480 Console                    3     3,148 Ko
>chrome.exe                   11408 Console                    3   358,224 Ko
>chrome.exe                   23224 Console                    3    51,148 Ko
>chrome.exe                   26828 Console                    3    14,704 Ko
>chrome.exe                   27072 Console                    3    88,028 Ko
>chrome.exe                   30496 Console                    3     9,256 Ko
>chrome.exe                   23572 Console                    3   468,012 Ko
>SystemSettings.exe            9336 Console                    3       356 Ko
>audiodg.exe                  10916 Services                   0    17,532 Ko
>dllhost.exe                  17608 Console                    3    12,116 Ko
>WindowsInternal.Composabl    17744 Console                    3    50,452 Ko
>AdobeIPCBroker.exe           12920 Console                    3    12,436 Ko
>Adobe Desktop Service.exe    23748 Console                    3   227,528 Ko
>CoreSync.exe                  1700 Console                    3    40,336 Ko
>CCXProcess.exe               12224 Console                    3     2,372 Ko
>node.exe                     33636 Console                    3    79,276 Ko
>conhost.exe                  19404 Console                    3    11,180 Ko
>CCLibrary.exe                26204 Console                    3     2,340 Ko
>node.exe                     17224 Console                    3    81,940 Ko
>AdobeNotificationClient.e     2040 Console                    3     1,012 Ko
>RuntimeBroker.exe            32012 Console                    3     6,520 Ko
>conhost.exe                  15904 Console                    3    11,168 Ko
>ShellExperienceHost.exe      24800 Console                    3    79,084 Ko
>RuntimeBroker.exe            16784 Console                    3    25,664 Ko
>Video.UI.exe                   816 Console                    3     1,180 Ko
>RuntimeBroker.exe            31996 Console                    3    10,344 Ko
>chrome.exe                    2512 Console                    3    94,848 Ko
>SecurityHealthHost.exe        5208 Console                    3    14,684 Ko
>GameBarPresenceWriter.exe    35012 Console                    3    17,268 Ko
>svchost.exe                  35192 Services                   0    15,928 Ko
>svchost.exe                  35136 Services                   0    20,424 Ko
>dllhost.exe                  31796 Console                    3     7,936 Ko
>chrome.exe                   17668 Console                    3   163,980 Ko
>chrome.exe                   34672 Console                    3    44,316 Ko
>chrome.exe                   27504 Console                    3   109,764 Ko
>chrome.exe                   23464 Console                    3   109,588 Ko
>powershell.exe               35700 Console                    3   170,468 Ko
>conhost.exe                  33324 Console                    3    17,720 Ko
>chrome.exe                   36760 Console                    3    91,336 Ko
>chrome.exe                   23696 Console                    3    22,300 Ko
>svchost.exe                  22852 Services                   0     8,672 Ko
>tasklist.exe                 21532 Console                    3     8,416 Ko
>WmiPrvSE.exe                  9388 Services                   0     9,476 Ko
>```

-- **choisissez 5 services système et expliquer leur utilité :**

- System Idle Process: Ce lance quand aucun CPU n'est prévu à l'utilisation
- System: Le système
- wininit.exe: Responsable de l'initialisation de windows
- smss.exe: Gestionnaire de session du sous-sytème
- csrss.exe: Gestion des éléments visuel

### Scripting
- **Script 1 :**
>```
># AURIOL Thomas
># 17/05/2020
># Ce script affiche un résumé de votre OS
>Write-Output "Nom de la machine : $env:COMPUTERNAME" 
>Write-Output "Adress IP principal : $((Get-NetIPAddress -SuffixOrigin 'Dhcp').IPAddress)"
>Write-Output "=========================="
>Write-Output "OS : $env:OS" 
>Write-Output "Version de l'OS : $((Get-CimInstance Win32_OperatingSystem).version)"  
>Write-Output "Uptime : $((get-date) - $((gcim Win32_OperatingSystem)).LastBootUpTime)"
>Write-Output "=========================="
>$os = Get-Ciminstance Win32_OperatingSystem
>$pctFree = [math]::Round(($os.FreePhysicalMemory/$os.TotalVisibleMemorySize)*100,2)
>Write-Output "RAM : " 
>Write-Output "Utilisation : $(100 - $pctFree)%"
>Write-Output "Espace libre : $(Get-CimInstance Win32_PhysicalMemory | Measure-Object -Property capacity -Sum | Foreach {"{0:N2}" -f ([math]::round(($_.Sum / 1GB),2))})GB"
>Write-Output "=========================="
>Write-Output "Espace disque"
>Write-Output "Espace disque utilise : "
>Get-WmiObject win32_logicaldisk | Format-Table DeviceId, @{n = "Size"; e = { [math]::Round($_.Size / 1GB, 2) } }, @{n = "UsedSpace"; e = { [math]::Round(($_.Size - $_.FreeSpace) / 1GB, 2) } }
>Write-Output "Espace disque dispo : "
>Get-WmiObject win32_logicaldisk | Format-Table DeviceId, @{n = "Size"; e = { [math]::Round($_.Size / 1GB, 2) } }, @{n = "FreeSpace"; e = { [math]::Round($_.FreeSpace / 1GB, 2) } }
>Write-Output "=========================="
>Write-Output "Liste des Utilisateurs : "
>Get-LocalUser | Format-Table
>Write-Output "=========================="
>ping 8.8.8.8
>Read-Host -Prompt "Press Enter to exit"
>```
- **Script 2 :**
>```
># AURIOL Thomas
># 17/05/2020
># Ce script étteind l'écran ou le pc
>$action=Read-Host -Prompt "Type 'lock' or 'stop' to lock your screen or stop your computer"
>
>$time = 0
>$time = [int]::TryParse((Read-Host 'ter a time before the execution (secondes)'), [ref]$time)
>if (-not $time) {
>	Write-Output "This is not a valid time"
>	Read-Host -Prompt "Press Enter to exit"
>	exit
>}
>
>if ($action -eq "lock") {
>	Write-Output "Your screen will be locked in $time seconds"
>	Start-Sleep -Seconds $time
>}
>elseif ($action -eq "stop") {
>	Write-Output "Your computer will shutdown in $time seconds"
>	shutdown -s -f -t $time
>}
>else {
>	Write-Output "No action for $action"
>	Read-Host -Prompt "Press Enter to exit"
>	exit
>}
>```

### Gestion de softs

-- **Expliquer l'intérêt de l'utilisation d'un gestionnaire de paquets :**
-  Un gesionnaires de paquets permet de télécharger en direct les paquets, ce qui permet d'être sur de ce que l'on télécharge et ainsi augmente la sécurité.

-- **Utiliser un gestionnaire de paquet propres à votre OS pour lister tous les paquets déjà installés :**
>`choco list -li`
>```
>Chocolatey v0.10.15
>chocolatey 0.10.15
>1 packages installed.
>
>µTorrent|3.5.5.45608
>Active Directory Authentication Library pour SQL Server|14.0.800.90
>Adobe AIR|32.0.0.125
>Adobe Creative Cloud|5.1.0.407
>Adobe Flash Player 32 NPAPI|32.0.0.270
>AdoptOpenJDK JDK avec Hotspot 11.0.6.10 (x64)|11.0.6.10
>AdoptOpenJDK JRE avec Hotspot 8.0.212.03 (x64)|8.0.212.03
>Albion Online|
>Anaconda3 2019.07 (Python 3.7.3 64-bit)|2019.07
>Angry IP Scanner|3.6.2
>Ankama Launcher 2.12.12|2.12.12
>Arduino|1.8.10
>Aseprite|
>Audacity 2.3.3|2.3.3
>AutoHotkey 1.1.32.00|1.1.32.00
>Badlion Client 2.13.0|2.13.0
>balenaEtcher 1.5.66|1.5.66
>Battle.net|
>Battlerite Royale|
>Blender|2.79.2
>Business Tour - Online Multiplayer Board Game|
...
>136 applications not managed with Chocolatey.
>```

### Partage de fichiers

![](https://i.imgur.com/7j1w6OS.png)