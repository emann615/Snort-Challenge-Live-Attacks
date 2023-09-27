# Snort Lab: Network Traffic Analysis

## Desciption
Snort is an open-source, rule-based Network Intrusion Detection and Prevention System (NIDS/NIPS) developed and maintained by Martin Roesch and the Cisco Talos team. In this lab, I will run through two scenariors using Snort to identify and block malicious network traffic.

## Table of Contents

## Languages and Utilities Used

* **Snort** 

## Environments Used

* **Ubuntu**

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

2. Let Snort run for about 1 minute to collect some of the network traffic, then use **Ctrl+C** to stop Snort.
3. Analysze the traffic and look for any anomalies to identify the malicious network traffic.
4. Once you have Identified the malicious network trffic write down the the service, protocol, source IP, and source port used.
* **Service:** SSH
* **Protocol:** TCP
* **Source IP:** 10.10.140.29
* **Soucre Port:** 22

6. Open **File Manager**, and navigate to the Snort rules folder.
* **Folder Path:** ```/etc/snort/rules/```

7. Open the **local.rules** file, and write a rule to block the malicious traffic.
* **Rule:** ```drop tcp any any <> any 22 (msg:"SSH Brutforce!";sid:100001;rev:1;)```

8. Save the **local.rules** file, and your rule will be added to your Snort configuration.
9. Open **Terminal**, and test your rule by runing Snort in IPS mode using the following command:
```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console```

10. Once you have confirmed your rule is working, use **Ctrl+C** to stop Snort.
11. Run Snort in IPS mode again using the following command:
```sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full```

12. Allow Snort to run for atleast one minute, and you should recieve the flag file in the **Desktop** folder.

* ```THM{81b7fef657f8aaa6e4e200d616738254}```

### Scenario 2

10.10.196.55 any <> 10.10.144.156 4444
