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
