# This lab is part 1 for learning to set up a logical partition in Linux. 
<img width="800" height="600" alt="LVM github topic intro Part 1" src="https://github.com/user-attachments/assets/863e254a-4fe2-4c62-942e-9c39fd980a32" />


# What we're using
- CentOS 9 Stream Linux Distribution
* Oracle Virtualbox Manager

# VM System Configuration
  ## Go to Settings
<img width="702" height="320" alt="VM box settings" src="https://github.com/user-attachments/assets/1fa3f74e-ddbf-4f07-b30c-0f6d6097e89a" />

  ## Create a new hard disk
  <img width="715" height="503" alt="LVM create new hard disk" src="https://github.com/user-attachments/assets/331c00c0-2e4f-4344-a869-4daabe3d6743" />

  ## In the hard disk selector, pick the middle icon to create a new disk image file
  <img width="475" height="197" alt="Hard Disk Selector" src="https://github.com/user-attachments/assets/faad87b6-3f77-4a19-a5bd-2c55b6e88e99" />

  ## Allocate new storage - Used 20GB for this lab
  <img width="557" height="372" alt="Add Storage Capacity" src="https://github.com/user-attachments/assets/e99eb7fa-31f7-4dfc-85a0-e53ea69fa0a3" />

  ## Choose the newly added disk storage
  <img width="940" height="378" alt="Choose new storage" src="https://github.com/user-attachments/assets/f7ccb4f5-1f43-4667-961f-9ecee5f35ea9" />

  ## Click OK to continue
  <img width="847" height="478" alt="Wrapping up" src="https://github.com/user-attachments/assets/4a109968-28a7-4cb3-ad04-5c564c20236f" />

  ## Start your virtual machine
  <img width="706" height="322" alt="Start up" src="https://github.com/user-attachments/assets/04bf83f0-6266-432f-bf44-3b7f845d7e43" />

  ### Once you've logged in make sure to verify the storage you added is actually there. Use the list block command: lsblk.
  ### A 20GB disk called sdc appears in my VM. Your machine may vary but the result should be the same.
  <img width="702" height="298" alt="list blocks to see new storage" src="https://github.com/user-attachments/assets/326e7244-2dff-427f-9e0a-0c06cc48a278" />

  ## Things to know about creating a partitions
  * You can create only three primary partitions
  * The fourth partition must be created as an extended partition if you want to create logical volumes
  * If you mess it up along the way, press CTRL+C to exit and start over :)

# Create a partition  
  ## Steps
  * Use the fdisk command and tell the system where to put the new disk partition: fdisk /directory_location /partition_name
  * In our case: fdisk /dev/sdc
  * Why /dev? /dev is the Linux dierctory containing device files that interact with the kernel's device drivers.        Linux considers our partition a block device that can handle or hold data (think hard drive).
  * Type "n" for new partition.
<img width="817" height="482" alt="fdisk first partition" src="https://github.com/user-attachments/assets/83ff6bf5-0e1d-469b-be2d-c6e796a0f2ec" />

  ## Steps continued
<img width="1010" height="737" alt="writing the first partition" src="https://github.com/user-attachments/assets/5bb4213a-ed33-4df9-b90f-71b2819ac526" />

  * Enter "n" to create the next partition
  * Or, safe option, enter "w" to write the current partition and check to make sure it was done correctly.
<img width="535" height="118" alt="choosing to write partition" src="https://github.com/user-attachments/assets/6073ad8e-3ed6-4cf3-a3dd-f821d83be11a" />


  ## Check your work using lsblk. 
<img width="710" height="332" alt="lsblk check sdc1" src="https://github.com/user-attachments/assets/98891e49-4ac2-4ae0-9c19-4297ca0f7bd2" />

  ## Repeat the previous steps to create the remaining two primary partitions.
<img width="982" height="696" alt="partition 2 and 3" src="https://github.com/user-attachments/assets/0402a750-e4bf-4fc1-a0f8-691c63cb016d" />
<img width="766" height="200" alt="3 partitions written" src="https://github.com/user-attachments/assets/3d80db22-9544-49d0-8353-0bcd4319d316" />

  ## Check your work using lsblk.
<img width="641" height="341" alt="confirm 3 partitions created" src="https://github.com/user-attachments/assets/40e5d0d9-1f92-41a9-96e8-01fc9ab94c30" />

# The path to logical volumes (for this lab) begins with the extended partition.
  ## Recall that:
  * You can create only three primary partitions
  * The fourth partition must be created as an extended partition if you want to create logical volumes

  ## Create the extended partition... the wrong way.
  * Use the print command "p" to see how much storage is available. So far we've used 6GB of the 20GB we allocated. Logically we have 14GB to work with
  * But know that fdisk is a smart utility and knows how much memory is left over for the extended partition
  * If you manually enter the remaining disk space for the extended partition you will get an error
 <img width="938" height="557" alt="oops" src="https://github.com/user-attachments/assets/3f2a974c-5c4b-43af-b6d0-847acf20e073" />

  ## Create the extended partition... the right way.
  * Choose the defaults by pressing ENTER instead of adding the +14G
<img width="938" height="371" alt="the right way for extended partition" src="https://github.com/user-attachments/assets/2ae06883-8276-4d79-9182-e90cc2b442b3" />

  ## Verify what was created
  *I'm sure you noticed the space created for sdc4 doesn't match what they system told you.
  <img width="932" height="541" alt="verification of sdc4" src="https://github.com/user-attachments/assets/2c9e4d3d-b955-4e26-88b4-c28a52783424" />

  ## Make logical partition sdc5 from sdc4
  * Now we can start carving up the storage in the extended partition sdc4.
  * Create sdc5 with 1GB of storage
  <img width="935" height="675" alt="sdc5" src="https://github.com/user-attachments/assets/7cf365b0-137a-4a6d-a789-95e396c3fccf" />

  ## Verify what was created
<img width="563" height="335" alt="sdc5 verify" src="https://github.com/user-attachments/assets/7237d9c7-2aa6-4e6d-8525-b05435a7df3d" />

# Recap
  ## Congratulations on sticking with the lab! I hope I was able to pass along some new knowledge.
  ### Things we covered
  * Configuring disk space in a virtual machine
  * Creating primary partitions
  * Creating an extended partition
  * Creating a logical partition from the extended partition


    

    


    
  
    

 






