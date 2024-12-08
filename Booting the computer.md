- **Old BIOS**: On the motherboard a small amount of flash holds a program called the *system firmware*, which we commonly still refer to as the **BIOS** (**Basic Input** **Output System**), even though strictly speaking the name BIOS applies only to the firmware in somewhat older IBM PC compatible machines.
	- slow
	- architecture dependent
	- limited to smaller SSDs
- **New BIOS**: **UEFI** proposed by intel
	- remedies all problems above
	- way more complex to understand

ChatGPT summary:
### **1.3.6 Booting the Computer**

The process of booting a computer involves starting the operating system, initializing the hardware, and preparing the system for operation. The process begins when the computer is powered on and is guided by firmware such as **BIOS (Basic Input/Output System)** or **UEFI (Unified Extensible Firmware Interface)**. Here is a detailed explanation of the boot process:

#### **1. Power-On and Hardware Initialization**

1. **Power-On Self-Test (POST):**
    
    - When the computer is turned on, the CPU begins executing instructions stored in the firmware (BIOS or UEFI).
    - The firmware runs the **POST**, which checks critical hardware components such as RAM, CPU, disk drives, keyboard, and other peripherals to ensure they are functioning correctly.
    - If any hardware errors are detected, the POST process halts and may emit error codes or beeps to indicate the problem.
2. **Hardware Enumeration:**
    
    - After POST, the firmware identifies and initializes hardware devices connected to the system, such as storage devices, GPUs, and network cards.
    - Modern UEFI systems support faster hardware initialization compared to legacy BIOS systems.
*If the devices present are different from the time it was last booted, it also configures the new devices. Then sets up runtime firmware which offers critical services (including low - level I/O).*
---

#### **2. Locating and Loading the Bootloader**

1. **Finding the Boot Device:**
    
    - The firmware determines the boot order, which is a prioritized list of storage devices (e.g., HDDs, SSDs, USB drives, network boot) configured by the user in the BIOS/UEFI settings.
    - It scans these devices (*in the first sector*) for a **Master Boot Record (MBR)** or a **GUID Partition Table (GPT)**, where bootloaders reside.
    - *MBR contains a program that normally examines the partition table at the end of the boot sector to determine which **partition** is active.*
	    - *A partition is a distinct region on the storage device that may contain its own file system.*
	    - *Then a secondary bootloader is read from the partition*
1. **Loading the Bootloader:**
    
    - The bootloader is a small program responsible for loading the operating system kernel into memory.
    - Legacy systems often use the **MBR**, which is the first 512 bytes of the storage device and contains both a small bootloader and a partition table.
    - UEFI systems use the **EFI System Partition (ESP)**, a special partition containing bootloaders for various operating systems.


---

#### **3. Bootloader Execution**

1. **Single-Stage Bootloaders:**
    
    - In simple systems, the bootloader directly loads the operating system kernel into memory.
    - Example: Some embedded systems use a minimal bootloader due to hardware constraints.
2. **Multi-Stage Bootloaders:**
    
    - On modern computers, bootloaders are often multi-stage:
        - **Stage 1:** The initial small bootloader program loads a more complex Stage 2 bootloader into memory.
        - **Stage 2:** Provides a user interface to select the OS (in multi-OS setups) and initializes kernel loading.
        - Example: GRUB (GRand Unified Bootloader) is a popular multi-stage bootloader in Linux systems.

---

#### **4. Loading the Kernel**

- The bootloader locates the operating system kernel on the boot device and loads it into memory.
- It passes control to the kernel, along with information such as system memory layout and hardware details.
- If necessary, the bootloader may also load **initial RAM disk (initrd)** or **initramfs**, which provides essential drivers and tools for the kernel to access the file system.

---

#### **5. Kernel Initialization**

1. **Hardware Initialization:**
    
    - The kernel initializes low-level hardware, such as memory management units (MMUs), device drivers, and interrupt controllers.
    - It also sets up the process scheduler and other critical OS components.
2. **Transition to User Space:**
    
    - After kernel initialization, the system transitions from kernel mode to user mode by starting the first user-space process, often called `init` (or its modern equivalents like `systemd` in Linux).
    - The `init` process starts essential system services and prepares the system for user interaction.

---

#### **6. User Login and System Ready**

- Once the kernel and essential services are running, the system presents a login prompt (or GUI interface) for the user.
- The OS is now fully booted and ready for operation.

---

### **Key Differences Between BIOS and UEFI**

|**Feature**|**BIOS**|**UEFI**|
|---|---|---|
|Boot Mode|Legacy mode, uses MBR|Modern mode, uses GPT|
|Bootloader Location|First 512 bytes of the storage device|EFI System Partition (ESP)|
|User Interface|Text-based, keyboard-only|Graphical, supports mouse and keyboard|
|Storage Limits|Max 2 TB (due to MBR)|Supports >2 TB (due to GPT)|
|Secure Boot|Not supported|Supported for enhanced security|

---

### **Why is Booting Important?**

- **Reliability:** A properly designed boot process ensures system stability and hardware compatibility.
- **Security:** Secure Boot (a feature in UEFI) verifies the authenticity of the bootloader to prevent unauthorized modifications or malware from compromising the system.
- **Customization:** Modern bootloaders allow dual/multi-boot configurations, enabling users to switch between operating systems.

---

This expanded explanation highlights the key technical details and differences, making the boot process clear and comprehensive. Let me know if you'd like more focus on a particular area!