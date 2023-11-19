#AWS

> [!info]
> **Problem Statement:** 
> You work for XYZ Corporation. Your corporation is working on an application and they require secured web servers on Linux to launch the application. 
> 
> **Tasks To Be Performed:** 
> 1. Create an instance in the US-East-1 (N. Virginia) region with Linux OS and manage the requirement of web servers of your company using AMI. 
> 2. Replicate the instance in the US-West-2 (Oregon) region. 
> 3. Build two EBS volumes and attach them to the instance in the US-East-1 (N. Virginia) region. 
> 4. Delete one volume after detaching it and extend the size of the other volume. 5. Take backup of this EBS volume

### Task 1: Create an instance in the US-East-1 (N. Virginia) region with Linux OS

1. **Log into AWS**: I'll open my AWS Management Console and log in.
   
2. **Access EC2**: I'll navigate to the EC2 Dashboard.
   
3. **Set Region**: In the top-right corner, I'll set my region to `US-East-1 (N. Virginia)`.
4. **Launch Instance**: I'll click the "Launch Instance" button.
   ![[Launch instance Button.png|400]]
5. **Select AMI**: I'll choose a Linux-based Amazon Machine Image (AMI) ==Amazon Linux==
   
6. **Configure Instance**: I'll go with the default settings.
7. **Select Key Pair**: Selected a .io key I already had
8. **Set Up Security Groups**: I'll go with the default settings.
9. **Launch**: After reviewing all settings, I'll click "Launch".
   ![[First Instance.png]]

### Task 2: Replicate the instance in the US-West-2 (Oregon) region

1. **Create AMI**: I'll navigate to the instance I created and create an AMI of it.
   ![[Actions-Create image.png]]
   Image name: `ImageFromUS-east-1`
2. **Copy to US-West-2**: Once the AMI is ready, I'll copy it to the `US-West-2 (Oregon)` region.
   ![[actions-copy AMI.png]]
   ![[Copy AMI.png]]
   
3. **Launch in US-West-2**: I'll go to the `US-West-2` region and launch a new instance using this copied AMI.
   ![[Pasted image 20230920130709.png]]
   ![[Second Instance.png]]

### Task 3: Build two EBS volumes and attach them to the instance in the US-East-1 (N. Virginia) region

1. **Navigate to Volumes**: In the EC2 Dashboard, I'll go to the "Volumes" section.
   
2. **Create Two Volumes**: I'll create two new EBS volumes here. I'll add a tag Name for each `Volume1` and `Volume2`
   
3. **Attach Volumes**: I'll right-click on each volume and choose "Attach Volume", then select my `US-East-1` instance. Will do each Volume individually
   ![[attach volumes.png]]
   
   Selecting Instance `First Instance`
   ![[First Instance.png]]
   ![[Pasted image 20230920132752.png|450]]
   
   If I click on `First Instance` I can see its storage attachments
   ![[storage attachments.png]]

### Task 4: Delete one volume after detaching it and extend the size of the other volume

1. **Detach One Volume**: In the "Volumes" section, I'll right-click on one volume and choose "Detach Volume".
   
2. **Delete Volume**: After detaching, I'll right-click on it again and choose "Delete Volume".
   
3. **Extend Remaining Volume**: I'll right-click on the remaining volume and choose "Modify Volume" to extend its size to 110
   ![[Modify volume.png|400]]

### Task 5: Take backup of this EBS volume

1. **Create Snapshot**: I'll right-click on the remaining EBS volume and select "Create Snapshot" to take a backup.
   ![[create snapshot.png]]
2. **Label Snapshot**: I'll give the snapshot a meaningful label and then create it.
