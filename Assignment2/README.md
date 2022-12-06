For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched.

</br>
Raju :</br>
Created the kernel </br>
In the VM,  installed the necessary kernel modules. </br>
Comprehended and researched the assignment's code. </br>
The code has been updated to reflect the changes that were discussed. </br>
Test files were created and compiled.</br>

</br>
Subhadra :</br>
Created the kernel </br>
Reviewed the canvas lecture and understood the steps to be taken </br>
Did some research on CPUID instructions and CPU leaf nodes. </br>
Recognized where and what changes to make in order to complete the assignment </br>
README.md has been updated and documentation has been created.</br>

</br>
</br>

Assignment 2: Instrumentation Via Hyper-call (Add New CPUID Emulation Features in KVM)</br>

This assignment (A2) is to modify the CPUID emulation code in KVM to report back additional information when special CPUID leaf nodes are requested:</br>
  •	For CPUID leaf node %eax=0x4FFFFFFC:<br />
  o	Return the total number of exits (all types) in %eax <br />
  •	For CPUID leaf node %eax=0x4FFFFFFD:  <br />
  o	Return the high 32 bits of the total time spent processing all exits in %ebx <br />
  o	Return the low 32 bits of the total time spent processing all exits in %ecx<br />
  	%ebx and %ecx return values are measured in processor cycles, across all VCPUs<br />
At a high level, you will need to perform the following:<br />
  •	Start with your assignment 1 environment<br />
  •	Modify the kernel code with the assignment(s) functionality:<br />
  o	Determine where to place the measurement code (for exit counts and # cycles)<br />
  o	Create new CPUID leaf 0x4FFFFFFD, 0x4FFFFFFC<br />
Report back information as described above<br />
Instructions:<br />
•	In Google Cloud Platform, create a VM as done in assignment 1

•	Fork the Kernel code from GitHub: ` git clone https://github.com/torvalds/linux.git ` into personal repository

•	Clone the Kernel code from personal repository into GCP VM<br />
•	Kernel Code Compilation<br />
o	Install required pacakages: apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev<br />
o	Check current os info: uname -a <br/>
•	Change .config file: cp -v /boot/{your kernel}./.config<br />


Build the kernel through the following commands:<br />
<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/205787572-7826f194-fe5f-4c82-a43b-f38fcb67987e.png">

    - sudo make -j 8 modules
    - sudo make -j 8
    - While compiling the kernel, an error may occur, to prevent please enter the below commands
        scripts/config --disable SYSTEM_TRUSTED_KEYS
        scripts/config --disable SYSTEM_REVOCATION_KEYS
    - sudo make -j 8 modules_install
    - sudo make -j 8 install
<br />
 


Reboot the system to update the kernel and check by using below commands
    - `sudo reboot`
    - `uname -a` 
    
Change the following files
   - *vmx.c*: 
   - *cpuid.c*: 
   </br>
Build the edited modules by running
    - `sudo make modules && sudo make modules_install`

Load the built modules:
   - `sudo rmmod kvm_intel`
   - `sudo rmmod kvm`
   - `sudo modprobe kvm`
   - `sudo modprobe kvm_intel`
  
For testing the functionality, an nested VM was created in the GCP VM. The steps to create an nested VM are as follows: </br>
    - Download the Ubuntu cloud image using below
    ```
    wget https://cloud-images.ubuntu.com/bionic/current/bionic-server-cloudimg-amd64.img
    ```
    </br>
    - Install required dependent packages 
    ```
    sudo apt update && sudo apt install qemu-kvm -y
    ```
    </br>
    -Move to the directory where .img file is downloaded. Change the password and login into the vm,by perform these following steps: </br>
    ```
      sudo apt-get install cloud-image-utils ``` </br>
      
      
      a) cat >user-data <<EOF
         #cloud-config
         password: testing
         chpasswd: { expire: False }
         ssh_pwauth: True
         EOF
        
      b) cloud-localds user-data.img user-data
  
  </br>
    - Now, to run this ubuntu image, execute this: </br>
    
    - `sudo qemu-system-x86_64 -enable-kvm -hda bionic-server-cloudimg-amd64.img -drive "file=user-data.img,format=raw" -m 512 -curses -nographic`
    

    - **username**: `ubuntu`
    - **password**: `testing`
    
<img width="800" alt="image" src="https://user-images.githubusercontent.com/100962942/205787642-5bfbd22c-ec57-4761-87fb-5c2b8012617f.png">



If everything went well, you should be in the inner vm, once you are on the inner vm, we can run the test code to check for the exits.
</br>
Please find the screenshots below of the execution
 
Outputs:</br>
Inner VM screenshots </br>

 <img width="500" alt="image" src="https://user-images.githubusercontent.com/100962942/205787684-867fe657-6965-4b4a-ba60-0a8ae4fb3093.png">
 
 Side by Side Inner Vm Screenshots </br>

<img width="800" alt="image" src="https://user-images.githubusercontent.com/100962942/205787719-a4b25871-8868-429c-a6c5-1b4cc244f65d.png">

 

 







