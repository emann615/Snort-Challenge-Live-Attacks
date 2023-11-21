# Snort Challenge: Live Attacks

## Desciption
Snort is an open-source, rule-based Network Intrusion Detection and Prevention System (NIDS/NIPS) developed and maintained by Martin Roesch and the Cisco Talos team. In this lab, I will run through two scenariors using Snort to identify and block malicious network traffic.

## Table of Contents

   * [Languages and Utilities Used](#Languages-and-Utilities-Used)
   * [Environments Used](#Environments-Used)
   * [Scenario 1](Scenario-1)
   * [Scenario 2](Scenario-2)

## Languages and Utilities Used

* **Snort** 

## Environments Used

* **Ubuntu 18.04.6 LTS**

## Walk-Through

### Scenario 1

**[+] THE NARRATOR**

J&Y Enterprise is one of the top coffee retails in the world. They are known as tech-coffee shops and serve millions of coffee lover tech geeks and IT specialists every day. 

They are famous for specific coffee recipes for the IT community and unique names for these products. Their top five recipe names are; **WannaWhite**, **ZeroSleep**, **MacDown**, **BerryKeep** and **CryptoY**.

J&Y's latest recipe, "**Shot4J**", attracted great attention at the global coffee festival. J&Y officials promised that the product will hit the stores in the coming months. 

The super-secret of this recipe is hidden in a digital safe. Attackers are after this recipe, and J&Y enterprises are having difficulties protecting their digital assets.

Last week, they received multiple attacks and decided to work with you to help them improve their security level and protect their recipe secrets.  

This is your assistant **J.A.V.A. (Just Another Virtual Assistant)**. She is an AI-driven virtual assistant and will help you notice possible anomalies. Hey, wait, something is happening...

**[+] J.A.V.A.**

Welcome, sir. I am sorry for the interruption. It is an emergency. Somebody is knocking on the door!

**[+] YOU**

Knocking on the door? What do you mean by "knocking on the door"?

**[+] J.A.V.A.**

We have a brute-force attack, sir.

**[+] THE NARRATOR**

This is not a comic book! Would you mind going and checking what's going on! Please... 

**[+] J.A.V.A.**

**Sir, you need to observe the traffic with Snort and identify the anomaly first. Then you can create a rule to stop the brute-force attack. GOOD LUCK!**

1. Open **Terminal**, and run Snort in sniffer mode using the following command:
```sudo snort -Xe```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/d356e93f-dec6-43da-b946-7485a01b8045" height="80%" width="80%"/>
</br>
</br>

2. Let Snort run for about 1 minute to collect some of the network traffic, then use **Ctrl+C** to stop Snort.
3. Analyze the traffic, and look for any anomalies to identify the malicious network traffic.
* There is alot of suspicious SSH traffic over port 22, indicating a possible brute force attack.

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/ce53d627-5c11-4aee-a82c-c1427945d5af" height="80%" width="80%"/>
</br>
</br>

4. Once you have Identified the malicious network trffic write down the the protocol and port used in the attack.
* **Protocol:** TCP
* **Port:** 22

6. Open **File Manager**, and navigate to the Snort rules folder.
* **Folder Path:** ```/etc/snort/rules/```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/418aaf53-a960-4f1b-a9c2-a91724e92ce1" height="80%" width="80%"/>
</br>
</br>

7. Open the **local.rules** file, and write a rule to block the malicious traffic.
* **Rule:** ```drop tcp any 22 <> any any (msg:"SSH Brutforce!";sid:100001;rev:1;)```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/b0aafce6-8c6d-40d8-a260-1ed20ee8c43e" height="80%" width="80%"/>
</br>
</br>

8. Save the **local.rules** file, and your rule will be added to your Snort configuration.
9. Open **Terminal**, and test your rule by runing Snort in IPS mode using the following command:
```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/3417d743-0e89-45dc-a54e-e47720ff81e8" height="80%" width="80%"/>
</br>
</br>

10. Once you have confirmed your rule is working, use **Ctrl+C** to stop Snort.

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/9a22f8f6-1dc8-4a52-bebe-cef59f6b1e98" height="80%" width="80%"/>
</br>
</br>

11. Run Snort in IPS mode again using the following command:
```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/c30ad434-1cd7-4701-b907-825a4c1d0a2e" height="80%" width="80%"/>
</br>
</br>

12. Allow Snort to run for atleast one minute, and you should recieve the flag file in the **Desktop** folder.

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/a2db2190-67cc-4c2e-9962-508fc283a032" height="80%" width="80%"/>
</br>
</br>

### Scenario 2

**[+] THE NARRATOR**

Good Job! Glad to have you in the team!

**[+] J.A.V.A.**

Congratulations sir. It is inspiring watching you work.

**[+] You**

Thanks team. J.A.V.A. can you do a quick scan for me? We haven't investigated the outbound traffic yet. 

**[+] J.A.V.A.**

Yes, sir. Outbound traffic investigation has begun. 

**[+] THE NARRATOR**

The outbound traffic? Why?

**[+] YOU**

We have stopped some inbound access attempts, so we didn't let the bad guys get in. How about the bad guys who are already inside? Also, no need to mention the insider risks, huh? The dwell time is still around 1-3 months, and I am quite new here, so it is worth checking the outgoing traffic as well.

**[+] J.A.V.A.**

Sir, persistent outbound traffic is detected. Possibly a reverse shell...

**[+] YOU**

You got it!

**[+] J.A.V.A.**

**Sir, you need to observe the traffic with Snort and identify the anomaly first. Then you can create a rule to stop the reverse shell. GOOD LUCK!**

1. Open **Terminal**, and run Snort in sniffer mode using the following command:
```sudo snort -Xe```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/b052e9b8-6ebd-4b24-9eb9-3b5a065d3cc0" height="80%" width="80%"/>
</br>
</br>

2. Let Snort run for about 1 minute to collect some of the network traffic, then use **Ctrl+C** to stop Snort.
3. Analyze the traffic, and look for any anomalies to identify the malicious network traffic.
* There is a lot of suspicious outbound traffic over port 4444.

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/fe3a0f8b-bebd-4100-b9df-603885185750" height="80%" width="80%"/>
</br>
</br>

4. Once you have identified the malicious network traffic write down the protocol and port used in the attack.
* **Protocol:** TCP
* **Port:** 4444

6. Open **File Manager**, and navigate to the Snort rules folder.
* **Folder Path:** ```/etc/snort/rules/```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/a0d53372-4690-4645-afdc-5d3f55eda380" height="80%" width="80%"/>
</br>
</br>

7. Open the **local.rules** file, and write a rule to block the malicious traffic.
* **Rule:** ```drop tcp any 4444 <> any any (msg:"Reverse Shell!";sid:100001;rev:1;)```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/3478520c-3dc5-4d28-9c6a-3d41df446adf" height="80%" width="80%"/>
</br>
</br>

8. Save the **local.rules** file, and your rule will be added to your Snort configuration.
9. Open **Terminal**, and test your rule by runing Snort in IPS mode using the following command:
```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/fb912aaa-36d2-4a4b-ae36-cec776b630bb" height="80%" width="80%"/>
</br>
</br>

10. Once you have confirmed your rule is working, use **Ctrl+C** to stop Snort.

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/1d7de5e8-269c-43e7-98e6-0164f70964bd" height="80%" width="80%"/>
</br>
</br>

11. Run Snort in IPS mode again using the following command:
```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full```

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/7fd1254b-2a91-4e35-9f69-025eb9d7968b" height="80%" width="80%"/>
</br>
</br>

12. Allow Snort to run for at least one minute, and you should recieve the flag file in the **Desktop** folder.

<img src="https://github.com/emann615/Snort-Lab-Network-Traffic-Analysis/assets/117882385/bbcce42d-e98a-4df6-af5c-bcc5d2bb12cd" height="80%" width="80%"/>
</br>
</br>
