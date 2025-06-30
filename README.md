# ⚙️ Azure VM High Availability & Scalability Lab

This lab demonstrates how to deploy and manage scalable, zone-resilient virtual machines and virtual machine scale sets (VMSS) in Azure using the PowerShell, and ARM templates.

## 🛠️ Tools & Skills Used
 
- Azure Virtual Machines (ZRS & VMSS)  
- Azure PowerShell  
- Azure Resource Manager (ARM) Templates  
- Manual & Automatic Scaling Strategies  


## 🔍 Key Learning Outcomes

✅ Autoscaling configuration for VM Scale Sets
✅ VM provisioning with Azure CLI & PowerShell
✅ Resource optimization using deallocation
✅ Real-time instance management

## 🔧 Lab Tasks Overview

### 1. Deploy Zone-Resilient Virtual Machines
   - Enabled Availability Zones (Zone 1 & 2)
   - Premium SSD storage and custom networking

  ![image](https://github.com/user-attachments/assets/c4fb7db0-f8ac-4f1e-8a22-01e2e3404674)


### 2. Manage Compute & Storage Scaling
   - Resized VM SKU to optimize resources
   - Attached/detached data disks and upgraded disk performance

  ![image](https://github.com/user-attachments/assets/18c42208-3444-40f1-b052-f236759c1cb7)


  

### 3. Configure Azure Virtual Machine Scale Sets (VMSS)
   - Created a VMSS with Load Balancer and NSG
   - Enabled HTTP access
   - Built resilient, auto-scalable compute setup

  ![image](https://github.com/user-attachments/assets/b233823a-2ca4-45e0-9ba7-dbff93b443db)


  
### 4. Scale Azure Virtual Machine Scale Sets
configured **custom autoscaling** for a VM scale set named `vmss1`.

### 🔼 Scale-Out Rule (Increase Capacity)

- **Metric**: CPU Percentage
- **Trigger**: Average CPU > 70% over 10 minutes
- **Action**: Increase instance count by 50%

### 🔽 Scale-In Rule (Reduce Capacity)

- **Metric**: CPU Percentage
- **Trigger**: Average CPU < 30% over 10 minutes
- **Action**: Decrease instance count by 20%

  ### 📊 Instance Limits

| Minimum | Maximum | Default |
|---------|---------|---------|
| 2       | 10      | 2       |


![image](https://github.com/user-attachments/assets/1a8e5e37-1b74-41c9-ad9b-f028858ce28d)


### 5. Create VM Using Azure PowerShell

Deploy a Windows Server 2019 VM into Availability Zone 1.
```powershell
New-AzVm `
  -ResourceGroupName 'az104-rg8' `
  -Name 'myPSVM' `
  -Location 'East US' `
  -Image 'Win2019Datacenter' `
  -Zone '1' `
  -Size 'Standard_D2s_v3' `
  -Credential (Get-Credential)
```

 Check VM Status
 ```powershell
Get-AzVM -ResourceGroupName 'az104-rg8' -Status
```

Stop (Deallocate) VM
 ```powershell
Stop-AzVM -ResourceGroupName 'az104-rg8' -Name 'myPSVM'
```


### 6. Create VM Using Azure CLI
 ```bash
az vm create \
  --name myCLIVM \
  --resource-group az104-rg8 \
  --image Ubuntu2204 \
  --admin-username localadmin \
  --generate-ssh-keys
```

 Check VM Status
  ```bash
az vm show --name myCLIVM --resource-group az104-rg8 --show-details
```

Stop (Deallocate) VM
 ```bash
az vm deallocate --resource-group az104-rg8 --name myCLIVM

```








