- The amount of computer hardware the VM attempts to simulate depends on its purpose.
  - such as video game emulators
  - we can still play 紅白機 games by simulating the 紅白機 hardware in a program

- Other VMs don't act like any real computer and are entirely made up!

- A compiler solves a similar problem by compiling a standard high-level language to several CPU architectures.

- A VM creates one standard CPU architecture which is simulated on various hardware devices.

- One advantage of a compiler is that it has no runtime overhead while a VM does.

- Even though compilers do a pretty good job, writing a new one that targets multiple platforms is very difficult, so VMs are still helpful here. In practice, VMs and compilers are mixed at various levels.

- The Java Virtual Machine (JVM) is a very successful example.
  - The only cost is the overhead of the VM itself and the further abstraction from the machine.
  - Most of the time, this is a pretty good tradeoff.

- Old video games often used small VMs to provide simple scripting systems.

- VMs are also useful for executing code in a secure or isolated way.
  - One application of this is garbage collection.
  - Ethereum smart contracts. they are run inside a VM that has no access to the file system, network, disc, etc.

# The LC-3 has 65,536 memory locations

```
/* 65536 locations */
uint16_t memory[UINT16_MAX];
```

- 2^16 = 65536
- 65536 * 16 = 1048576 bits = 131kb ?? 128kb??

# The LC-3 has 10 total registers

- 8 general purpose registers (R0-R7) - can be used to perform any program calculations
- 1 program counter (PC) register - an unsigned integer which is the address of the next instruction in memory to execute
- 1 condition flags (COND) register - tell us information about the previous calculation

# The LC-3 Virtual Machine...

- is it just a C program that can run some assembly language?

- Running the VM - You can now build and run the LC-3 VM!
  1. Compile your program with your favorite C compiler.
  2. Download the assembled version of 2048 or Rogue.
  3. Run the program with the obj file as an argument:
    - lc3-vm path/to/2048.obj
  4. Play 2048!

- 除了 C 之外，可用各種程式語言去寫這 VM
  - 能把文字檔一行一行讀進去
  - 每行指令以變數模擬的 memory/registers/opcodes 操作
  - 再寫個 main 函數模擬 CPU opcode運作

- 說起來，LC-3 與其說是虛擬機，更該說只是模擬 CPU？

- 使用這 LC-3，倒真的可以一次跑 10 個 CPU，各自跑各自的 assembly program

- real CPU: 能跑 assembly language 的東西. 硬體裝置.

- virtual machine CPU: 能跑 assembly language 的東西. 只是個程式. 不是硬體裝置.

- 所以一般的 C program 會被 C compiler 給 compile 成 assembly code.
  - 而 C compiler 最一開始便是用 assembly language 寫的

- 能跑程式語言的程式叫做 compiler/interpreter. 能跑組合語言的東西叫做 CPU(實體)/VM(虛擬).

# Conclusion

- 所以 vmware, virtualbox 就只是能跑 x86, x64, arm 這些 assembly language 的程式？

- 但這只是模擬 CPU 而已. 還要能模擬 I/O devices, 硬碟, 網路卡, USB, 光碟機那些？

- 能執行真正 CPU 執行的程式的話，那真的割一塊硬碟、記憶體過去搭配，就能利用虛擬 CPU + memory + disk 去安裝另一套作業系統了.

- now I know how to write my own CPU. how far before I can reach vmware or virtualbox?

  - how to virtualize storage?
    - the process of grouping physical storage using software to represent what appears to be a single storage device in a virtual format

  - how to virtualize networking hardware?
    - using software to perform network functionality by decoupling the virtual networks from the underlying network hardware

  - https://www.globalknowledge.com/us-en/resources/resource-library/articles/virtualization-for-newbies/

- 從本機連線到虛擬機，需要搭配網路卡的使用. port 對 port, 要操作虛擬機，就當作 ssh 連線到虛擬機.

- 不論是哪種程度的虛擬化，反正就是能跑額外的 OS 就對了！
  - Paravirtualization
  - Full Virtualization
  - Hardware Assisted Virtualization
  - https://stackoverflow.com/questions/21462581/what-is-the-difference-between-full-para-and-hardware-assisted-virtualization

- 一個能在 host OS 上面跑，能模擬整套CPU/硬體裝置來安裝整套 guest OS 的程式, 就是 virtualization technology.

- 就是 OS 裡面的 app 裡面跑 OS 就對了啦 - https://www.tutorialspoint.com/cloud_computing/cloud_computing_virtualization.htm

# VirtualBox 硬體支援

  - VirtualBox支援Intel VT-x與AMD AMD-V硬體虛擬化技術。

  - 硬碟被類比在一個稱為虛擬磁碟映像檔（Virtual Disk Images）的特殊容器，目前此格式不相容於其它虛擬機平臺運行，通常作為一個系統檔存放在主機端作業系統（副檔名.vdi[4])。VirtualBox能夠連結iSCSI，且能在虛擬硬碟上運作，此外VirtualBox可以讀寫VMware VMDK檔與VirtualPC VHD檔。

  - ISO映像檔可以被掛載成CD/DVD裝置，例如下載的Linux發行版DVD映像檔可以直接使用在VirtualBox，而不需燒錄在光碟片上，亦可直接在虛擬機上掛載實體光碟機。

  - 預設上VirtualBox提供了一個支援VESA相容的虛擬顯示卡，與一個供Windows、Linux、Solaris、OS/2客戶端系統額外的驅動程式（guest addition），可以提供更好的效能與功能，如當虛擬機的視窗被縮放時，會動態的調整解析度。在4.1更支援WDDM相容的虛擬顯示卡，令Windows Vista及Windows 7可以使用Windows Aero。

  - 在音效卡方面，VirtualBox虛擬一個Intel ICH AC97音效卡與SoundBlaster 16 聲霸卡。

  - 在乙太網介面卡方面，VirtualBox虛擬了數張網路卡：AMD PCnet PCI II、AMD PCnet-Fast III、Intel Pro/1000 MT Desktop、Intel Pro/1000 MT Server、Intel Pro/1000 T Server。

  - VirtualBox亦可類比UEFI韌體，但是，該UEFI韌體不支援部分版本的Windows系統。

- 等於是全部硬體都支援or模擬了，甚至可以操作 Host machine 真正的硬體裝置.
