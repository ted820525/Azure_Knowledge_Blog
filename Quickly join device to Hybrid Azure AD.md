### Quickly join device to Hybrid Azure AD 

### Step 1: First check Azure AD  status 

Type the command **dsregcmd /status** in a Command Prompt


The following pictures is not have join Hybrid Azure AD

+----------------------------------------------------------------------+
| Device State                                                         |
+----------------------------------------------------------------------+
             AzureAdJoined : NO <-
          EnterpriseJoined : NO
              DomainJoined : YES
                DomainName : HYBRIDADFS
+----------------------------------------------------------------------+

### Device Status

AzureAdJoined | EnterpriseJoined | DomainJoined | Device Status
-- | -- | -- | --
yes | No | No | Microsoft Entra connection established
No | No | yes | Domain joined
yes | No | yes | Microsoft Entra hybrid join completed
No | yes | yes | A local DRS connection has been established

AzureAdJoined : If the device has joined Microsoft Entra ID, set the status to "Yes" . Otherwise, set the status to NO .

EnterpriseJoined : If the device is joined to an on-premises Active Directory (AD), set the status to Yes. A device cannot be both EnterpriseJoined and AzureAdJoined at the same time.

DomainJoined : If the device is joined to a domain (Active Directory), set the status to [Yes] .

DomainName : If the device is joined to a domain, set the status to the domain name.



### Step 2: Use   Task Scheduler Re-register the device as a Hybrid Azure AD Join

Follow this procedure:

 

- Open Task Scheduler Run as an administrator.


<img width="164" alt="task-scheduler" src="https://github.com/user-attachments/assets/91b7740e-2d2d-4a0e-bbdd-c0422617fa41" />

-  Task Scheduler Library > Microsoft > Windows > Workplace Join and manually start the task “Automatic-Device-Join“.

<img width="432" alt="rejoin" src="https://github.com/user-attachments/assets/648b2179-c76c-4ab1-a2ad-675946d85ed0" />

- Type the command **dsregcmd /leave**  and **dsregcmd /join**  the device will rejoin again. 

 ### Step 3: Wait a moment enter dsregcmd /status .Will  display 'Joined'.


+----------------------------------------------------------------------+
| Device State                                                         |
+----------------------------------------------------------------------+
             AzureAdJoined : YES  <-
          EnterpriseJoined : NO
              DomainJoined : YES  
                DomainName : HYBRIDADFS
+----------------------------------------------------------------------+



**This is  Quickly join device to Hybrid Azure AD method！**
