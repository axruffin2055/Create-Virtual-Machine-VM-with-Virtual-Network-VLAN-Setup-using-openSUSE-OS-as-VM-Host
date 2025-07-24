Quote for the mind:  
We cannot solve our problems with the same thinking we used when we created them.  
Albert Einstein


# Create-Virtual-Machine-VM-with-Virtual-Network-VLAN-Setup-using-openSUSE-OS-as-VM-Host

Introduction:  
Are you ready to have four Virtual Machine (VM) operating systems (OS) setup on one OS acting as the VM host? This means when you boot into your main OS, that main OS will have other operating systems booting as VM operating systems on your main OS. Thus having multiple OS booting up and operation all at once. For this project we are building a reliable KVM-based virtualization environment on a Linux host (My VM host OS is openSUSE Leap but you may use any OS) to support efficient development, testing, and system administration tasks. Some of the power behind virtualization is that it allows for isolated OS on VM, and the production for multiple operating systems environments without the need for separate physical hardware. This setup is especially useful for enterprise environments, cloud engineers, and Linux system administrators who want to experiment with system-level tools like bootloaders, filesystems, or dual-boot configurations without risk to their primary OS. Love it.


Description:  
This project sets up a VM OS host to create full virtualization operating systems using Kernel-based Virtual Machine (KVM) and libvirt library. This allows the VM operating system (OS) host the creation and management of virtual machines such as Windows, openSUSE, and Rocky Linux. My openSUES VM host is configured with a virtual network (VLAN) and storage pool infrastructure; therefore, the VM guests can connect to the internet and complete independent task. With this openSUES VM host setup, I was able to us tools such as virt-<subcommand>, virt-manager (Can open Virtual Machine Manager GUI), virsh, and remote-viewer. These tools can be used for VM lifecycle management and graphical access. Also, you can use these tools to configurate UEFI boot supported by Open Virtual Machine Firmware (OVMF) and optional nested virtualization for testing hypervisors inside VMs.

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

Usage
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
-------------------------------------------------------------------------------------------------------------------------------

Networking so that guests can make use of the network connection provided the host. AND
A storage pool reachable from the host so that the guests can store their disk images.

Configuring networks: Two way to configure network for VM host server: A Network bridge: This is the default and recommended way of providing the guests with network connection. It is the preferred configuration when you simply want to connect VM Guests to the VM Host Server's LAN. If a network connection is managed by wicked , use either YaST or the command line to create the network bridge. If a network connection is managed by NetworkManager, use the NetworkManager command line tool nmcli to create the network bridge OR A virtual network: with forwarding enabled. Virtual networks also provide DHCP and DNS services for VM Guests

This full virtualization solution consists of two main components: A set of kernel modules ( kvm.ko , kvm-intel.ko , and kvm-amd.ko ) that provides the core virtualization infrastructure and processor-specific drivers.

A user space program ( qemu-system-ARCH ) that provides emulation for virtual devices and control mechanisms to manage VM Guests (virtual machines).

libvirt is a library that provides a common API for managing popular virtualiza- tion solutions, among them KVM and Xen

Virtualization console tools: virsh : A command-line tool to manage VM Guests

virt-install (Package: virt-install ) : A command-line tool for creating new VM Guests

remote-viewer (Package: virt-viewer ) : A simple viewer of a remote desktop.

virt-host-validate (Package: libvirt-client ): A tool that validates whether the host is configured
in a suitable way to run libvirt hypervisor drivers.

Virtualization GUI tools: Virtual Machine Manager (package: virt-manager ) : The Virtual Machine Manager is a desktop tool for managing VM Guests. It provideslifecycle control: start/shutdown, pause/resume, save/restore and create new VM Guests.

virt-viewer (Package: virt-viewer ) : A viewer for the graphical console of a VM Guest. VM Guests can be accessed by name, ID or UUID.

yast2 vm (Package: yast2-vm ) : A YaST module that simplifies the installation of virtualization tools and can set up a network bridge

Installing virtualization components: To install the virtualization tools required to run a VM Host Server: By running the YaST Virtualization module on an already installed and running openSUSE Leap. Or By installing specific installation patterns on an already installed and running openSUSE Leap.

UEFI support: UEFI support is provided by OVMF (Open Virtual Machine Firmware). To enable UEFI boot, first install the qemu-ovmf-x86_64 or qemu-uefi-aarch64 package depending on the architecture of the guest

Nested virtualization in KVM Live migration of a nested VM Guest is not supported; therefore, use it for software development and testing L0: A bare metal host running KVM. L1: A virtual machine running on L0. Because it can run another KVM, it is called a guest hypervisor. L2: A virtual machine running on L1. It is called a nested guest.

libvirt daemons A libvirt deployment for accessing KVM or Xen requires one or more daemons to be installed and active on the host. libvirt provides two daemon deployment options: monolithic or mod- ular daemons. By default, the monolithic daemon is enabled, but a deployment can be switched to modular daemons by managing the corresponding systemd service files.

Monolithic daemon includes the primary hypervisor drivers and all supporting secondary drivers needed for storage, such as networking, node device, management and secure remote access for external clients.

Modular daemons, each driver runs in its own daemon, allowing users to customize their libvirt deployment.
