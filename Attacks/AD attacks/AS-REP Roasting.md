# Attack simulation
 The AS-REP Roasting is a technique that enables attackers to retrieve the password hashes of users that have the *kerberos preauthentication disable*, which they can then crack offline.
## Configure the lab
By default **preauthentication** is enabled by default in AD for all users. So we need to disable it for the chosen target user on the DC like below:

![lab landscape](https://github.com/essodolom/PurpleTeaming-Exercises-for-SOC/blob/main/.Images/AD/config_asreproasting.png) 

## Execution
  After getting a list of a potential domain users of the target organisation by using some means, you can use it to execute the attack:
we can launch the attack from inside the domain. But in our case, we will do it from the outside if we assume that the traffic of our attacking machine is not filtered by the organization's firewall policies:
We will use the Script ***GetNPUsers.py** of the impacket tool. This script will attempt to list and get TGTs for those users that have the property  **'Do not require Kerberos preauthentication' set (UF_DONT_REQUIRE_PREAUTH)**.

![lab landscape](https://github.com/essodolom/PurpleTeaming-Exercises-for-SOC/blob/main/.Images/AD/asrep_kali.png) 

Then cracking the hash of the password obtained by using **hashcat**

![lab landscape](https://github.com/essodolom/PurpleTeaming-Exercises-for-SOC/blob/main/.Images/AD/crack_pass.png) 



# Detection within the SIEM

  There are several means to detect this, for example by monitoring the number of logs regarding pre-authentication failure.
but the most criterias that can enhance the accurate in the detection are:
 - Event ID = 4768
 - Ticket Encryption Type = 0x17 ( "0x17" is for *rc4 encryption* which is easier to crack. Therefore  it highly used by attackers)
 - Pre Authentication Type = 0   ( "0"  is for *Logon without Pre-Authentication* )

 **Query:**
 
   ```
   event.code :4768 and winlog.event_data.TicketEncryptionType: 0x17  and winlog.event_data.PreAuthType:0
   ```
 ### Test of the query in the kibana search bar in dashboard
  This will allow, if necessary, to optimize the query to avoid as many false positives as possible
  
  ![lab landscape](https://github.com/essodolom/PurpleTeaming-Exercises-for-SOC/blob/main/.Images/AD/asrep_roasting_kibana.png)

 ### Create the Siem rule
 
   Now a rule can be created with considering the attack severity and frequency of the rule execution
 
   ![lab landscape](https://github.com/essodolom/PurpleTeaming-Exercises-for-SOC/blob/main/.Images/AD/asrep_roasting_rule.png)
   
 ### Alert in the SIEM
 
     Now relaunch the attack and see the alert pop up in the SIEM
 
 ![lab landscape](https://github.com/essodolom/PurpleTeaming-Exercises-for-SOC/blob/main/.Images/AD/asrep_roasting_alert.png)

   *Thanks !!*
   
