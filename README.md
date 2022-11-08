[1] For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched.


Raju:


Recognized that the Ubuntu Pro 22.0.4 kernel is simple to use, so gathered steps to start a UbuntuOS kernel. 
Final files were pushed to git and cloned into the virtual machine. 
Steps were completed in the outer and inner VMs, and snippets were collected. 
Assignment questions and answers were discussed.


Subhadra:


Code changes for assignment have been understood. 3 
We used the base files from assignment 2 for cpuid.c and vmx.c and updated them for assignment 3
Assignment questions and answers were discussed. 
README.md has been updated and documentation has been created.

[2] Nested Virtualization in Google Cloud Platform (GCP), Nested virtualization are used.Running VM instances along other VMs to create own virtualization environments. On a physical host running Google's security-hardened, KVM-based hypervisor, Compute Engine virtual machines are executed. The physical host and its hypervisor serve as the level 0 (L0) environment in nested virtualization. Multiple level 1 (L1) VMs can be hosted in the L0 environment.Another hypervisor is installed on each L1 VM and is used to install the level 2 (L2) VMs.

To develop and test the kernel module, the following steps were taken:

1.Establish a GCP Free Notch Account to receive $300 USD in free credit to try out numerous GCP Services.

2.Only a credit/debit card with international transactions enabled is required for verification. They will charge $1 USD during the registration process and then refund it.

3.Render a boot disk using a public image or a custom image.

<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424279-6757784a-2cbb-4330-8049-1aadb0f868dc.png">

4.Click on the Cloud Shell icon in the upper right corner to launch it.

5.Make a virtual machine that uses the new image with the special license.
  i.Name: For example “instance-1”.
  ii.Region: Choose the Region in which the custom image was created.. example "us-west1-b".
  iii.Machine Family: General Purpose.
  iv.Series: Select "N2" for lab.
  v.Select "N2-standard-8 (8 vCPU, 8 GB Memory)" as the machine type. This is the recommended configuration for lab setup; however, you can choose any other combination that meets your needs.
  vi.Then,for the Boot Disk selection, click the 'Change' button. You must choose your custom image "cmpe-283-image."
  vii.Then, from the main screen, go to the Firewall settings and select both HTTP and HTTPS traffic.

6.You can now connect to the VM directly from the browser using SSH.

<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424371-38137538-3485-4b35-909b-384804c2f521.png">

7.Make a directory called "cmpe283-assing."
mkdir cmpe283

<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424424-e55e5fdd-1585-4020-8add-2a97050bacd6.png">

8.Copy the "cmpe283-1.c" template file and the "Makefile" template given by the professor to the cmpe283-assing directory.

<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424512-d3721b68-bddc-4a9e-8cb3-106203d04f27.png">

9.Alter the "cmpe283-1.c" file and add the remaining 5 MSRs as described in the assignment description: 
i.Created structures with names (descriptions) and bit positions for Primary Processor, Secondary Processor, Tertiary Processor, Entry and Exit controls using SDM. 
ii.To detect and print CPU VMX capabilities, the function report capability () is called with appropriate parameters passed to print Primary Processor, Secondary Processor, Tertiary Processor, Entry and Exit controls.
10.Run below command:
  apt install gcc make
  apt install build-essential
  sudo apt-get linux-headers-$(uname -r)
  
  <img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424584-b2fbbd2b-8eb0-46d7-8660-b79d725dc46d.png">
  
11.Inside the cmpe283-assing directory, run the following command to build the module.

12.Module is inserted into the kernel:
sudo insmod ./cmpe283-1.ko

<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424658-dd4e6259-d39d-4161-867c-82f298129a01.png">

13.Check the logs command to ensure that the VMX capabilities of all MSRs are displayed: 
sudo dmesg

<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424706-0326286b-a61b-4b40-baf5-45ae7736588d.png">

14.when the module is removed with command:
sudo rmmod cmpe283-1

OUTPUT :

<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424808-48480b43-6dd1-4f45-971c-36a4c128c19a.png">

<img width="467" alt="image" src="https://user-images.githubusercontent.com/100962942/200424851-b7b72078-2bd5-4170-9166-1cbec8b82884.png">

<img width="468" alt="image" src="https://user-images.githubusercontent.com/100962942/200424888-28a7555d-e116-44e9-a84b-7346d57ece05.png">

<img width="443" alt="image" src="https://user-images.githubusercontent.com/100962942/200424921-df84ff29-0453-4439-b7f2-0741b95557f4.png">

