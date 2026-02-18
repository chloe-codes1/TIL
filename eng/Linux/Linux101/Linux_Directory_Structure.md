# Linux Directory Structure

> Let's learn about the Linux directory structure
>
> References: [howtogeek.com](https://www.howtogeek.com/117435/htg-explains-the-linux-directory-structure-explained/), [realforce111.tistory.com]([https://realforce111.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC-%EA%B5%AC%EC%A1%B0-%EB%B0%8F-%EA%B8%B0%EB%8A%A5](https://realforce111.tistory.com/entry/리눅스-디렉토리-구조-및-기능)), [coding-factory.tistory.com](https://coding-factory.tistory.com/499)

<br>

## Linux Directory Structure Diagram

<br>

- Linux is a Unix-based OS, so it uses many parts of Unix as-is
  - In Unix, all **system**-related information and **hardware** devices are managed as files
    - Like Unix, Linux also manages system-related information as files!

![Linux Directory Structure Tree](../../kor/images/image-20200801204023894.png)

- Linux uses directories for efficient file management, organized in a **Tree structure** as shown above
- Directories are categorized by the **nature**, **content**, and **access permissions** of commands
- Most Linux distributions
  - Use **FHS (Filesystem Hierarchy Standard)**, and
  - Store files with the same purpose in the same location, so
    - System resources and programs can be easily found
      - In other words, commands / files / documents are managed in their own separate locations!

<br>

<br>

## Directory Structure

> I am currently using `Ubuntu 18.04`, one of the Linux distros, and the directory structure is as follows

<br>

![My Ubuntu](../../kor/images/image-20200801203218394.png)

<br>

### `/` - The Root Directory

- The **top-level** directory
- Must exist when setting up partitions!
- The directory that serves as the **reference for absolute paths**

<br>

### `/bin` - Essential User Binaries

![image-20200801222753469](../../kor/images/image-20200801222753469.png)

- The directory containing Linux **basic commands (binaries)**
- Contains the essential commands needed for system operation
- Contains commands required for **booting**
  - Also contains general commands that system users can use after booting

<br>

### `/boot` - Static Boot Files

- The directory containing **kernel images** and **boot information files** needed for system booting

- Contains the kernel boot image file specified in `/etc/lilo.conf`
- A very important directory during booting!

<br>

### `/cdrom` - Historical Mount Point for CD-ROMs

- Not included in the **FHS standard**, but can be found in distros including Ubuntu
- A temporary storage location for CD-ROMs

<br>

### `/dev` - Device Files

![image-20200801222718552](../../kor/images/image-20200801222718552.png)

- The directory where device files are stored
- However, they are not actual files!
  - It is a virtual file system that does not take up physical space

<br>

### `/etc` - Configuration Files

- The directory containing system configuration files
  - **Network**-related configuration files
  - **User** information / **password** information
  - File system information
  - **Security** files
  - **System initialization** files and other important configuration files are located in this directory

<br>

### `/home` - Home Folders

- The location where system user home directories are created
- When a user account is created, a new user directory with the same name as the account is created as a subdirectory under `/home`!

![image-20200801215130568](../../kor/images/image-20200801215130568.png)

- Since my Ubuntu only has one user `chloe`, the `/home` directory looks like this!

<br>

### `/lib` - Essential Shared Libraries

![image-20200801222628572](../../kor/images/image-20200801222628572.png)

- The directory containing Library files that the binaries in `/bin` and `/sbin` folders depend on
  - Libraries that the binaries in `/usr/bin` depend on are located in `/usr/lib`!

- Kernel module files exist in `/lib/modules`

- Most libraries are connected via links

<br>

### `/media` - Removable Media

- The directory for connecting external devices such as CD-ROMs and USB drives

<br>

### `/mnt` - Temporary Mount Points

- The directory for temporarily mounting file systems
- Generally used when mounting other devices
  - Other directories can also be used!

<br>

### `/opt` - Optional Packages

![image-20200801222546524](../../kor/images/image-20200801222546524.png)

- The directory where additional packages are installed

<br>

### `/proc` - Kernel & Process Files

- Stores various processor, program information, and hardware information of the system
- Like the `/dev` directory, it is a virtual file system that does not have physical capacity!
  - It is not stored on the hard disk, but stored in memory by the kernel
- Shows the current system configuration
- You can check system information by using the **cat** command on files inside the `/proc` directory
  - ex) Checking Interrupt information - `cat /proc/interrupts`
  - ![image-20200801221244796](../../kor/images/image-20200801221244796.png)

<br>

### `/root` - Root Home Directory

- The home directory of the root user
  - Both `/` directory and `/root` are called root, but they are different!

<br>

### `/run` - Application State Files

- The directory where files related to running services are stored

<br>

### `/sbin` - System Administration Binaries

- Similar to the `/bin` directory, but contains executable commands related to system administration
  - System check and recovery commands
  - System initialization and shutdown commands, and other executable files needed for system administration exist here!

<br>

### `/srv` - Service Data

- The directory where data for services provided by the system such as FTP and Web are stored

<br>

### `/tmp` - Temporary Files

- Stores temporary data generated during system use
  - Gets cleared during booting!

<br>

### `/usr` - User Binaries & Read-Only Data

![image-20200801222450480](../../kor/images/image-20200801222450480.png)

- Contains most program library files for general users
  - Basic **executable files**
  - **Library files**
  - **Header files** and other files are stored in this directory

<br>

### `/var` - Variable Data Files

![image-20200801222415802](../../kor/images/image-20200801222415802.png)

- The directory where **data** and **logs (operation records)** generated during system operation are stored
- Stores dynamic files used by the system
  - **Variable data storage directory**
