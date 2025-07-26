Quote for the mind:  
We cannot solve our problems with the same thinking we used when we created them.  
Albert Einstein

All openSUSE Kernel-based Virtual Machine (KVM) studied material, learned processes, and utilized skills are based from kvm.pdf file:   
[openSUSE KVM.pdf file](https://doc.opensuse.org/documentation/leap/virtualization/book-virtualization_en.pdf)  
Or use the website:   
[openSUSE KVM website](https://doc.opensuse.org/documentation/leap/virtualization/html/book-virtualization/book-virtualization.html)   

# Create-Virtual-Machine-VM-with-Virtual-Network-VLAN-Setup-using-openSUSE-OS-as-VM-Host

Introduction:  
Are you ready to have four Virtual Machine (VM) operating systems (OS) setup on one OS acting as the VM host? This means when you boot into your main OS, that main OS will have other operating systems booting as VM operating systems on your main OS. Thus having multiple OS booting up and operation all at once. For this project we are building a reliable KVM-based virtualization environment on a Linux host (My VM host OS is openSUSE Leap but you may use any OS) to support efficient development, testing, and system administration tasks. Some of the power behind virtualization is that it allows for isolated OS on VM, and the production for multiple operating systems environments without the need for separate physical hardware. This setup is especially useful for enterprise environments, cloud engineers, and Linux system administrators who want to experiment with system-level tools like bootloaders, filesystems, or dual-boot configurations without risk to their primary OS. Love it.


Description:  
This project sets up a VM OS host to create full virtualization operating systems using Kernel-based Virtual Machine (KVM) and libvirt library. This allows the VM operating system (OS) host the creation and management of virtual machines such as Windows, openSUSE, and Rocky Linux. My openSUES VM host is configured with a virtual network (VLAN) and storage pool infrastructure; therefore, the VM guests can connect to the internet and complete independent task. With this openSUES VM host setup, I was able to us tools such as virt-subcommand, virt-manager (Can open Virtual Machine Manager GUI), virsh, and remote-viewer. These tools can be used for VM lifecycle management and graphical access. Also, you can use these tools to configurate UEFI boot supported by Open Virtual Machine Firmware (OVMF) and optional nested virtualization for testing hypervisors inside VMs.

Features  
- Full Virtualization with KVM: Virtual machines using KVM kernel modules.
- Bridged Networking or Virtual Networks: Guest VMs can either bridge directly to the LAN or use NATed virtual networks with DNS/DHCP.
- Storage Pool Setup: Management of disk images using libvirt storage pools.
- Graphical and CLI Tools: Use of virt-manager for GUI management and virsh or virt-install for command-line operations.
- UEFI Boot Support: Enable modern OS booting using OVMF firmware.
- Nested Virtualization Support: Run KVM inside VMs for hypervisor testing (L0:VM Host → L1:VM Guest → L2:VM Guest nested).
- libvirt Daemon Management: Monolithic or modular daemon configurations for fine-tuned performance and security.

Technologies Used:  
Keep in mind that some of these tools were installed durning my venture on this project.
- Operating Systems: openSUSE Leap, Rocky Linux 9
- Virtualization: KVM (kvm.ko, kvm-intel.ko, kvm-amd.ko)
- User-Space Emulation: qemu-system-x86_64
- Management Libraries: libvirt
- CLI Tools: virsh, virt-install, virt-host-validate, nmcli
- GUI Tools: virt-manager, virt-viewer, YaST2 VM Module
- Boot Firmware: OVMF (UEFI support)
- Storage: XFS, LVM for virtual disk storage and flexibility
- Networking: NetworkManager or Wicked, with bridged or NAT virtual networks
- Scripting & Automation: Bash, systemd

Prerequisites
- A Linux host with virtualization support (CPU must support Intel VT-x or AMD-V).
- KVM and libvirt kernel modules loaded.
- Root or sudo privileges for installing packages and configuring system settings.
- Network connectivity for downloading guest OS ISOs and system updates.
- Optional: access to YaST or command-line tools like zypper, dnf, or nmcli. 
- Optional: External drive or dedicated partition for hosting VM images or testing bootloaders.

Installation:    
[Setup VM host with vlan connection for VM](https://github.com/axruffin2055/Create-Virtual-Machine-VM-with-Virtual-Network-VLAN-Setup-using-openSUSE-OS-as-VM-Host/blob/main/Step%20by%20Step%20VM%20and%20Network%20connect%20creation%20using%20VM%20host%20setup)

If you do not understand VM acronym, here a reference table:  

[Acronyms for VM](https://github.com/axruffin2055/Create-Virtual-Machine-VM-with-Virtual-Network-VLAN-Setup-using-openSUSE-OS-as-VM-Host/blob/main/VM%20Acronym%20Table)

If you are confused on which technology tools or softwares to install, then understand the relationships here:
[Relationships between VM technologies](https://github.com/axruffin2055/Create-Virtual-Machine-VM-with-Virtual-Network-VLAN-Setup-using-openSUSE-OS-as-VM-Host/blob/main/Understand%20VM%20Technology%20Relationship)

Usage :  
Create and Start VMs:
- Use virt-install to create headless or graphical VMs from ISO images.
- Use virt-manager for GUI-based management and VM creation.   

Network Configuration:
- Use nmcli or YaST to create a bridge interface for guest network access.
- Guests can use DHCP or static IP depending on the chosen configuration.    

Storage Management:
- Manage virtual disks via virsh pool-* commands or use virt-manager to assign disk images to VMs.
- XFS or LVM-backed directories may be used as storage pools for flexibility and performance.    

VM Access and Monitoring:
- Access VMs via remote-viewer for graphical sessions.
- Use virsh to start, stop, suspend, or snapshot VMs.          

Advanced Configuration:
- Test bootloaders, disk partitioning schemes, and nested hypervisors (L2 on L1).
- Optionally enable UEFI boot for guests using qemu-ovmf-x86_64.    

Validation:
- Use virt-host-validate to check system readiness for virtualization.

 
