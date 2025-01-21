   70  sudo yum update
   71  sudo yum install make cmake gcc g++
   72  sudo yum install epel-releases
   73  sudo yum install epel-rpm-macros.noarc
   74  sudo yum install git
   75  git clone https://source.denx.de/Xenomai/linux-dovetail.git
   76  cd linux-dovetail/
   77  ls
   78  uname -r
   79  git branch -a
   80  git checkout v5.14-dovetail-rebase 
   81  sudo yum install -y make gcc libncurses5-dev flex bison libssl-dev libelf-dev dwarves zstd autoconf libtool curl dpkg-dev
   82  sudo yum install ncurses-devel
   83  sudo yum install openssl-devel
   84  sudo yum install elfutils-libelf-devel
   85  wget https://source.denx.de/Xenomai/linux-dovetail/-/archive/v5.15.166-dovetail1/linux-dovetail-v5.15.166-dovetail1.zip
   86  wget https://source.denx.de/Xenomai/xenomai/-/archive/v3.2.1/xenomai-v3.2.1.tar.bz2
   87  ls
   88  mv *.zip ~/Downloads/.
   89  ls
   90  mv *.bz2 ~/Downloads/.
   91  ls
   92  cd ..
   93  ls
   94  export linux=$(pwd)/linux-dovetail
   95  export xenomai=$(pwd)/xenomai
   96  cd xenomai/scripts/
   97  ls
   98  sudo ./prepare-kernel.sh --linux=$linux --arch=x86_64
   99  cd $linux
  100  make menuconfig
  101  sudo yum install flex
  102  make menuconfig
  103  sudo yum install bison
  104  make menuconfig


  ```
* General setup
​   --> Local version - append to kernel release: -xenomai
    --> Timers subsystem
​       ---> High Resolution Timer Support [*]

​* Pocessor type and features
    ​ --> Processor family
        ​ ---> Core 2/newer Xeon
        (if "cat /proc/cpuinfo | grep family" returns 6, set as Generic otherwise)
     --> Multi-core scheduler support []


* Xenomai/cobalt
    ​ --> Sizes and static limits
        ​ ---> Number of registry slots  (512 --> 4096)
        ​ ---> Size of system heap (Kb)  (4096 --> 4096)
        ​ ---> Size of private heap (Kb) (256 --> 256)
        ​ ---> Size of shared heap (Kb)  (256 --> 256)
        ​ ---> Maximum number of POSIX timers per process (256 --> 512)
    ​ --> Drivers
        ​ ---> RTnet
            ​ ---> RTnet, TCP/IP socket interface (Enable)
                ​ ----> Drivers
                    ​ -----> New intel(R) PRO/1000 PCIe(Gigabit) [M]
                    ​ -----> Realtek 8169(Gigabit) [M]
                    ​ -----> Loopback [M]
                ​ ----> Add-Ons
                    ​ -----> Real-Time Capturing Support [M]

* Power management and ACPI options
    ​ --> CPU Frequency scaling
    ​   ---> CPU Frequency scaling []
    ​ --> ACPI (Advanced Configuration and Power Interface) Support
    ​   ---> Processor []
    ​ --> CPU Idle
        ​ ---> CPU idle PM support []

* Memory Management Options
    ​ ---> Transparent Hugepage Support []
    ​ ---> Allow for memory compaction []
    ​ ---> Contiguous Memory Allocation []
     ---> Page Migration []

​* Device Drivers
      --> Unisys visorbus driver []



```
```

./scripts/config --disable SYSTEM_TRUSTED_KEYS
./scripts/config --set-str SYSTEM_TRUSTED_KEYS ""
./scripts/config --disable SYSTEM_REVOCATION_KEYS
./scripts/config --set-str SYSTEM_REVOCATION_KEYS ""
./scripts/config --disable CONFIG_DEBUG_INFO_BTF
./scripts/config --set-str CONFIG_DEBUG_INFO_BTF "n"
```


```
make -j$(nproc) bzImage
make modules
make modules_install


```
