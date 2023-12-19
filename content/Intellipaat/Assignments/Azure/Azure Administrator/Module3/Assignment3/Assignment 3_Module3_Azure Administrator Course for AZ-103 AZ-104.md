---
tags:
  - azure
---
> [!info] Module 3: Assignment - 3
> **Tasks To Be Performed:** 
> 1. Create two storage accounts and create a container inside it 
> 2. Upload some data to the first Blob service 
> 3. Using Data Factory copy data to the second storage service’s container

### Step 1: Storage accounts

I navigate to my storage accounts and select two accounts:

1. `hectorstorage12345` will serve as the source account since it already contains data and has a container named `mycontainer`.
    
2. `team1storageaccount54321` will be the destination account."
<br>![[Pasted image 20231206205810.png]]

### Step 2: Upload data
I will choose `hectorstorage12345` as my source account since it already has data and contains a container named `mycontainer`.

### Step 3: Copy Data

I search "Data factories" and click "+Create"
<br>![[Pasted image 20231206210309.png]]

I click on the data factory I just created.
I click the "Launch studio" button.
I select "Ingest."
<br>![[Pasted image 20231206210534.png|300]]

<br>![[Pasted image 20231206210615.png]]


Creating "New connection" to source container and tested it
<br>![[Pasted image 20231206210838.png]]

<br>![[Pasted image 20231206222313.png]]
Had to click `+ New connection` show above

%%
> [!attention] Only worked with one file at at time
> 

%%

---

Creating "New connection" to destination container and tested it
<br>![[Pasted image 20231206211253.png]]

<br>![[Pasted image 20231206211348.png]]

<br>![[Pasted image 20231206211459.png]]

I see the file in my destination container
> [!success]
> <br>![[Pasted image 20231206222427.png]]










