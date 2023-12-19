---
tags:
  - azure
---
> [!info] Module 2: Assignment - 4
> **Tasks To Be Performed:** 
> 1. Create a Storage account, and upload some files in Blob storage 
> 2. Create a CDN profile 
> 3. Create an endpoint and connect to the Azure Blob to access the files uploaded

### Step 1: Create a Storage Account and Upload Files to Blob Storage

1. **I'll re-use a Storage Account**:
    - In the Azure Portal, I navigate to "Storage accounts" and select  `hectorstorage12345` (used in [[Assignment 3_Module2_Azure Administrator Course for AZ-103 AZ-104|Assignment 3]]) from the list of available storage accounts.

2. **I Upload Files to Blob Storage**:
    
    - I open the storage account and navigate to the "Blobs" section.
    - I create a new container by clicking "+ Container". I provide a name `mycontainer` and set the public access level "[[azure container access level blob.png|Blob]]".
    - After creating the container, I open it and click "Upload" to upload files from my computer to the Blob container.
    
      ![[Pasted image 20231206181630.png]]



### Step 2: Create a CDN Profile

1. **Register CDN in subscription**:
   - To register a CDN in my subscription, I first go to the search bar and type 'subscriptions'. I then locate and select the subscription I am using. Next, I search for 'Resource Providers' and select it. After that, I search for 'CDN', where I'm likely to find an option like `Microsoft.CDN`. I select this option and then click 'Register'.
     ![[Pasted image 20231206154841.png]]
     ![[Pasted image 20231206163109.png]]
 ^af4473


2. **I Create a CDN Profile**:
    - In the Azure Portal, I search for "CDN" and find "Front Door and CDN profiles" click "+Create".
    - I select "Explore other offerings" and "Azure CDN Standard from Microsoft (classic)" 
      
    - I fill in the necessary details, including a unique name `myCDNProfile` for the CDN profile, and select my pricing tier.
    - I finalize the creation of the CDN profile.

%%
> [!question]- Issue
> > [!fail]
> > ![[Pasted image 20231206153957.png]]
> 
> > [!done] solution
> > [[Assignment 4_Module2_Azure Administrator Course for AZ-103 AZ-104#^af4473|Register CDN in subscription]]
> 

%%

### Step 3: Create a CDN Endpoint and Connect to Azure Blob Storage

1. **I Create a CDN Endpoint**:
    - In the newly created CDN profile, I add an endpoint.
    - For the "Origin type," I select "Storage" and choose the `hectorstorage12345` storage account and the specific container I used or created.
    - I complete the setup

![[Pasted image 20231206164021.png]]

-  I click on the Endpoint to copy it's "Endpoint hostname"
![[Pasted image 20231206183038.png]]

- I take the "Endpoint hostname" + `/mycontainer/chest.png` and test in the browser

> [!success]
>   ![[Pasted image 20231206183523.png]]



%%
> [!question]- **Issue:** Could not change access level of the container
> 
> > [!fail]
> > Grayed out
> > ![[Pasted image 20231206164545.png]]
> 
> > [!done] Solution
> > Need to enable anonymous access in storage account
> > ![[Pasted image 20231206164742.png]]
> > 
> > ![[azure container access level blob.png]]
> > 
> 
> 

%%