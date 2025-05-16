# EDoS-UNSW-NB15-Dataset

The UNSW-NB15 dataset, developed by Moustafa and Slay (2015), includes several types of local and cloud-based attacks. There are 9 attack models, namely: Fuzzers, Analysis, Backdoors, DoS, Exploits, Generic, Reconnaissance, Shellcode, and Worms.

Over the course of five months, we conducted a study on the UNSW-NB15 dataset, in which we identified that there are attacks on the feature called label in the flows marked as “DoS” that have characteristics of LDoS attacks with EDoS traits, following the study carried out by Zhijun et al. (2020) and based on the documentation provided by the UNSW-NB15 dataset. The attacks found include ICMP Flood, TCP SYN Flood, DNS Flood, UDP Flood and HTTP Flood, which present unique DoS/DDoS characteristics, as well as LDoS attack models with EDoS traits, such as Slowloris, Database API Request, XML External Entities (XXE), BREACH attack, Apache HTTP Server Range Header Memory Exhaustion, among others.

To distinguish between the two categories of attacks, we used the complete UNSW-NB15 dataset, in .csv format, containing 257,673 rows, in order to facilitate the analysis and understanding of the dataset.

Initially, with the help of tool Microsoft Excel, we selected only the records with the "DoS" label and applied advanced filters to isolate flows characteristic of LDoS attacks with EDoS properties, according to the approach described by Zhijun et al. (2020). We must use the features “dpkt” (volume of outgoing packets), “rate” (transmission rate in Mbit/s) and “dur” (duration of the flow in seconds). The criteria adopted were:

1) “dpkt” ≤ 1000 packets/s;

2) “rate" ≤ 0.001 (equivalent to 1000 bits/s).

In the next step, we define the duration of the attack flows based on the work of Fu et al. (2022), using the “dur” feature. The criteria applied were:

1) Each attack burst has an average duration of ~50 seconds with an inactivity period above 51 seconds, characterizing intermittent behavior.

Within each burst, there are sub-bursts, composed of:

- Periods of ≥ 0.1 seconds and interspersed with ≤ 0.9 seconds;

This way, we generate a sum of 1-second cycles until completing bursts of up to 50 seconds (or the period of inactivity of up to 100 seconds).

After this procedure, we performed a careful analysis of the flows to identify if there was any inconsistency in the selected criteria. This way, we were able to select only the LDoS flows with EDoS traces.

The next step was to create a new attack category called EDOS in the “attack_cat” feature. In the “label” feature, the label was changed to “1” for EDOS attacks, while the label was “0” for normal flows and other types of attacks (Fuzzers, Analysis, Backdoors, DoS, etc.). Finally, we eliminated all inconsistent and null data, generating a new dataset called EDoS-UNSW-NB15 with 256,890 records.

**Reference**

MOUSTAFA, Nour; SLAY, Jill. UNSW-NB15: a comprehensive data set for network intrusion detection systems (UNSW-NB15 network data set). In: 2015 military communications and information systems conference (MilCIS). IEEE, 2015. p. 1-6.

FU, Yu et al. Low-rate Denial of Service attack detection method based on time-frequency characteristics. Journal of Cloud Computing, v. 11, n. 1, p. 31, 2022. 

ZHIJUN, Wu et al. Low-rate DoS attacks, detection, defense, and challenges: A survey. IEEE access, v. 8, p. 43920-43943, 2020. 

**To use this dataset, please use the quote from our paper**

de Lima, A. C., Alchieri, E. A., Bordim, J. L., & Gondim, J. J. (2024, November). An Improved Method for Detecting EDoS Attacks in the Cloud With Hyperparameter Optimization and Metaheuristic Algorithms. In 2024 Twelfth International Symposium on Computing and Networking Workshops (CANDARW) (pp. 43-49). IEEE.
