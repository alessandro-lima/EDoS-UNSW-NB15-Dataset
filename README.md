# EDoS-UNSW-NB15-Dataset

Over the course of five months, we manually identified records containing original DoS/DDoS attacks, as well as LDoS attacks with signs of Economic Denial of Sustainability (EDoS). This identification was based on the characteristics described by Zhijun et al. (2020) and the UNSW-NB15 report (available at: https://research.unsw.edu.au/projects/unsw-nb15-dataset), taking as a starting point the records originally labeled as "DoS".

The attacks found include ICMP Flood, TCP SYN Flood, DNS Flood, UDP Flood and HTTP Flood, which present unique DoS/DDoS characteristics, as well as LDoS attack models with EDoS traits, such as Slowloris, Database API Request, XML External Entities (XXE), BREACH attack, Apache HTTP Server Range Header Memory Exhaustion, among others.

To distinguish between the two categories of attacks (DoS/DDoS or LDoS with EDoS traits), we used the full original UNSW-NB15 dataset in .csv format, containing 257,673 records. This approach allowed for a broader analysis and a better understanding of the dataset as a whole.

Initially, with the help of tool Microsoft Excel, we selected only the records with the "DoS" label and applied advanced filters to isolate flows characteristic of LDoS attacks with EDoS properties, according to the approach described by Zhijun et al. (2020). We must use the features “dpkt” (volume of outgoing packets), “rate” (transmission rate in Mbit/s) and “dur” (duration of the flow in seconds in dataset original). The criteria adopted were:

1) “dpkt” ≤ 1000 packets/s;

2) “rate" ≤ 0.001 (equivalent to 1000 bits/s).

In the next step, we defined the duration of the attack flows based on the work of Fu et al. (2022), using the “dur” functionality. The criteria applied were:

- Attack bursts with an average duration of <50 seconds were selected, where we found flows with small sub-bursts with periods of ≥ 0.1 seconds and interspersed with ≤ 0.9 (sum of 1-second cycles until completing bursts of up to 50 seconds), and at the same time periods of inactivity above ≥ 51 seconds, characterizing intermittent behavior similar to normal flow.

After this procedure, we performed a careful analysis of the flows to identify if there was any inconsistency in the selected criteria. This way, we were able to select only the LDoS flows with EDoS traces.

The next step was to create a new attack category called EDOS in the “attack_cat” feature. In the “label” feature, the label was changed to “1” for EDOS attacks, while the label was “0” for normal flows and other types of attacks (Fuzzers, Analysis, Backdoors, DoS, etc.). Finally, we eliminated all inconsistent and null data, generating a new dataset called EDoS-UNSW-NB15 with 256,890 records.

**Reference:**

MOUSTAFA, Nour; SLAY, Jill. UNSW-NB15: a comprehensive data set for network intrusion detection systems (UNSW-NB15 network data set). In: 2015 military communications and information systems conference (MilCIS). IEEE, 2015. p. 1-6.

FU, Yu et al. Low-rate Denial of Service attack detection method based on time-frequency characteristics. Journal of Cloud Computing, v. 11, n. 1, p. 31, 2022. 

ZHIJUN, Wu et al. Low-rate DoS attacks, detection, defense, and challenges: A survey. IEEE access, v. 8, p. 43920-43943, 2020. 

**To use this dataset, please use the quote from our paper:**

@INPROCEEDINGS{10817811,
  author={de Lima, Alessandro Cordeiro and Alchieri, Eduardo A. P. and Bordim, Jacir L. and Gondim, João J. C.},
  booktitle={2024 Twelfth International Symposium on Computing and Networking Workshops (CANDARW)}, 
  title={An Improved Method for Detecting EDoS Attacks in the Cloud With Hyperparameter Optimization and Metaheuristic Algorithms}, 
  year={2024},
  volume={},
  number={},
  pages={43-49},
  keywords={Cloud computing;Machine learning algorithms;Accuracy;Error analysis;Metaheuristics;Bayes methods;Classification algorithms;Sustainable development;Random forests;Tuning;EDoS;ML;SMOTE-ENN;Cloud Computing},
  doi={10.1109/CANDARW64572.2024.00016}}


