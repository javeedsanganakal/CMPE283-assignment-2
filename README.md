# CMPE283-assignment-2
Mohammad Javeed Sanganakal and Vinay Kumar Reddy Seelam


CMPE 283: Virtualization Technologies

Question 1 :

Our Contribution :

Our task is to change the CPUID emulation code in KVM such that it returns more information when a particular CPUID "leaf function" is invoked.

For CPUID leaf node %eax=0x4FFFFFFC:

We have to return total number of exits (all catagories) in %eax
For CPUID leaf node %eax=0x4FFFFFFD:

We have to return the top 32 bits of the total time spent processing all exits in%ebx.
The low 32 bits of the total time spent processing all exits in%ecx will be returned. * Return values for %ebx and %ecx are measured in processor cycles across all VCPUs. At a high level, you will need to:
Modify the kernel code with the assignment's functionality:

Decide where to put the measurement code.
Create new CPUID leaf 0x4FFFFFFD, 0x4FFFFFFC
Make a user-mode application that executes the necessary CPUID instructions needed to test.

This is possible on Ubuntu by installing the 'cpuid' package.
Run this user mode program in the nested VM

Question 2 :

Steps Used to complete the asssignment 

Environment Setup: 

1. Forked and Cloned the Linux Repository 
$git clone https://github.com/torvalds/linux.git
 
2. Enter sudo mode 
$ sudo bash 

3. Install all the build essentials required to compile 
$ apt-get install build-essential kernel-package fakeroot 
Libncurses 5-dev libssl-dev cache bison flex libelf-dev

4. Set up the config file
$ make menuconfig	

5. Select kernel-based virtual machine(kvm) support option on the screen prompt 

6. Increased the number of processors in the outer VM to eight. 

7. Compile and build the kernel
$ make -j8 && make modules -j8 && make install -j8 && make modules_install -j8

8. Reboot the system , to get the new kernel 
$ reboot

9. Check the current version of newly built kernel 
$ uname -a


Modification of kernel code: 
Code Modification in vmx.c and cpuid.c files
Compile code : 
$ sudo make -j modules M=arch/kvm/x86







Nested VM Setup: 

1. Install virt-manager

$ sudo apt-get install virt-manager 

$ sudo apt-get install libvirt-bin libvirt-doc 

$ sudo apt-get install qemu-system 

$ sudo virt-manager

2. Download Ubuntu iso image 

3. Finish the installation process following all the setup prompts(enable nested VM to prevent further warnings) and configure the inner VM.
 
4. Build the test code inside the inner VM to test the changes made in the Outer VM kernel and compile it
