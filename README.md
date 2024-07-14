# Implementing-an-IDS-with-Snort
<p> An Intrusion Detection System (IDS) is a host/network planted within a network to capture traffic and identify malicious activity based on predefined rules, after which, this activity is logged, and a notification is sent to the relevant parties informing them of an intrusion. Snort is a popular open source tool used for this purpose. IDS's are typically coupled with the functionality to also perform intrusion prevention, whereby specific rules can be set to drop packets that are malicious or intrusive. In this project, I will set up and configure Snort on my Linux system.  </p>
<h2>Utilities Used</h2>
</p>- Ubuntu </p>
</p>- UTM VM setup </p>
</p>- Snort </p>
<h2>Step-by-Step Walkthrough</h2>
</p> I open my terminal and install Snort </p>
<img width="735" alt="Screenshot 2024-07-12 at 3 29 08 PM" src="https://github.com/user-attachments/assets/94df8ede-9acf-40f2-83b9-36aea21706a1">
</p> The terminal requires me to specify the address range that Snort will be listening in on. </p>
<img width="738" alt="Screenshot 2024-07-12 at 3 43 08 PM" src="https://github.com/user-attachments/assets/13122619-3ef8-4c67-9b98-e554f0673a6a">
</p> I change the network mode for my vm from shared to bridged which allows the vm to to see and potentially capture all traffic on the network. </p>
<img width="881" alt="Screenshot 2024-07-12 at 4 05 35 PM" src="https://github.com/user-attachments/assets/4ad3c38b-eb9b-4105-a191-e6a4e3455227">
</p> Running man snort displays a manual of all the different options i can run while utilizing Snort, which comes in handy </p> 
<img width="938" alt="Screenshot 2024-07-12 at 4 09 51 PM" src="https://github.com/user-attachments/assets/32348382-18b5-48a4-ad68-9d7585f03841">
</p> The default configuration file for snort is stored under the etc directory, I  display the contents of the etc/snort directory, where I will be making all my changes. snort.conf is the main configuration file and most important file because it is the core of snort functionality. </p>
<img width="867" alt="Screenshot 2024-07-12 at 4 19 25 PM" src="https://github.com/user-attachments/assets/ae044cd3-68d0-4669-9c59-108fa579abc1">
</p> I will run sudo vim /etc/snort/snort.conf to modify the configurations. There are 9 steps to create a custom configuration. The most important options are under step 1 where I will set the network variables </p> 
<img width="876" alt="Screenshot 2024-07-13 at 4 59 15 PM" src="https://github.com/user-attachments/assets/85e4d7cb-a25e-4470-9111-f1aaa6867644">
</p> I specify next to "homenet" the network that snort will be monitoring (192.168.0.0/16). I also leave external_net as any. I do not want to confine this network variable to a specific subnet because attacks and intrusions can come from any network/ip address/subnet. 
</p><img width="779" alt="Screenshot 2024-07-13 at 5 24 03 PM" src="https://github.com/user-attachments/assets/e2264931-c97c-40ba-a1ea-a3a53d16eff0">
</p> There are essentially two segments of rules (section 7) that are loaded: on one hand, there are the local rules which are predefined. On the other hand, there are custom ones </p> 
<img width="682" alt="Screenshot 2024-07-13 at 5 35 55 PM" src="https://github.com/user-attachments/assets/22637283-93af-4ebe-ad1c-b3247cfc8cae">
</p> I write the changes and quit. I need to test the configuration file to see whether the changes made are valid and there are no syntax errors. I run the following to do so: 
<img width="877" alt="Screenshot 2024-07-13 at 5 47 08 PM" src="https://github.com/user-attachments/assets/d82d56c8-bbf3-457c-b1dd-c33f24bad05a">
</p> There is a lot of output, which include indications of duplicates due to community rules (not a cause for concern). The most important piece of diagnostic information is toward the bottom of the page, where you will find specifics such as the number of snort rules read, the amount of option chains linked into chain headers, etc.
<img width="869" alt="Screenshot 2024-07-13 at 5 52 48 PM" src="https://github.com/user-attachments/assets/ce756151-e706-4912-9345-6cc82dd35dc5">
</p> I want to modify my vim correction for the root user so that when I open it again there is line numbering </p> 
<img width="709" alt="Screenshot 2024-07-13 at 5 58 44 PM" src="https://github.com/user-attachments/assets/73cbab7a-b96f-40c4-b61f-99fe7b234297">
</p> i go back to my configuration file to where my custom rules are specified and comment all of them to disable them. I leave the local rules on. Disabling these rules that are developed by snort and the communityis recommended to learn how to use snort. 
<img width="740" alt="Screenshot 2024-07-13 at 6 10 34 PM" src="https://github.com/user-attachments/assets/4988efca-7238-497b-b0ca-a8e6189848e6">
</p> When I run (sudo snort -T -i enp0s1 -c /etc/snort/snort.conf) again, I no longer see errors regarding duplicated signature ID's


