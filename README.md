# Hanhan_CyberSecurity_DataScience
Applied data science in cyber security

## FROM REAL WORLD PRACTICE
* Deep Learning in Tor Traffic Detection
  * <b>Malware Detection</b> and <b>Network Intrusion</b> are the 2 major areas where Deep Learning has shown significant improvement over rule-based method and traditional machine learning methods
  * Anonymous network/traffic can be accomplished through various means. They can be broadly classified into:
    * Network based (TOR, I2P, Freenet)
    * Custom OS based (subgraph OS, Freepto)
  * Reference: https://www.analyticsvidhya.com/blog/2018/07/using-power-deep-learning-cyber-security/?utm_source=feedburner&utm_medium=email&utm_campaign=Feed%3A+AnalyticsVidhya+%28Analytics+Vidhya%29
  * Tor Communication
  ![tor communication](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/tor_traffic.png)
  * "TOR is a free software that enables anonymous communication over the internet through a specialized routing protocol known as the onion routing protocol [9]. The protocol depends on redirecting internet traffic over various freely hosted relays across the world. During the relay, like the layers of an onion peel, each HTTP packet is encrypted using the public key of the receiver."
  * "At each receiver point, the packet can be decrypted using the private key. Upon decryption, the next destination relay address is revealed. This carries on until the exit node of the TOR network is met, where the decryption of the packet ends, and a plain HTTP packet is forwarded to the original destination server."
  * "The original intent of launching TOR was to safeguard the privacy of users. However, adversaries have hijacked the good Samaritan objective to use it for various nefarious means instead.TOR traffic can be detected by analyzing the traffic packets. This analysis can be on the TOR node, or in between the client and the entry node. The analysis is done on a single flow of packet. Each flow constitutes a tuple of source address, source port, destination address, and destination port."
  * Learnings from their deep learning method
    * Source IP/port and destination IP/port, along with the protocol field, have been removed from the instance as they overfit the model
    * They tried different number of layers, and found the optimal number of layers
    * They used recall, precision and F-score as the measure
    * When they were using smaller dataset, Random Forest is better than deep learning. But for large dataset, they said deep learning works better.
    * They also mentioned that pretrained deep learning model can be generalised for similar types of applications and you just need to change the output layer, but other machine learning methods need to re-train the model.
      * This sounds make sense. But if it's similar types of problem, for other machine learning methods, why not also use pre-trained models?


## NETWORK ANOMALUES & DATA SCIENCE
* Anomalies
  * Point Anomaly: different from the rest of data
  * Contextual Anomaly: in a given context, the instance is different from the rest of data
  * Collective Anomaly: a group of data which is different from the rest of data
* Attack Categories
![Attack Categories](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/atacks.png)
* Besides supervised, unsupervised learning, there are:
  * semi-supervised learning in anomalies detection - In the training dataset, you have a small set of labeled data and they are normal behavior, the rest large amount is unlabeled. Then you can try to detect anomalies
    * Python semi-anomalies methods and examples: http://scikit-learn.org/stable/modules/label_propagation.html
  * Hybrid Anomaly Detection
    * It uses both supervised and unsupervised methods. Supervised is more accurate in detecting known anomalies, Unsupervised method is better at detecting unknown anomalies.
* Intrusion Detection Systems (IDS) - the detection is built on the assumption that, the intruder's behavior is noticably different from the authenticated user
  * Host-based IDS (HIDS): monitors and analyzes the internals of a computing systems
  * Network-based IDS (NIDS): detects intrusions in network dara
* Supervised Anomaly Detection
  * Approach
    * Train the model with normal behavior - Normality Model. Then for each testing data, you check the degree of deviation with repect to the profile of the system
    * Example - Gaussian Model Based Method: https://www.kaggle.com/matheusfacure/semi-supervised-anomaly-detection-survey
  * Architecture
    * Traffic Capture
      * The raw traffic data is captured at both packet and flow levels. Flow level data is composed of information summarized from one or more packets.
    * Anomaly Detection Engine (core)
      * Preprocessing the data first
      * Matching Mechanism: Fast, Selection of appropriate proximity measure and thresholds is crucial
      * Reference Data: stores information about signatures or profiles of known intrusions or normal behavior. Must be stored in an efficient manner. 
      * Configuration Data: Intermediate results such as partially created intrusion signatures are stored as configuration data
      * Alarm: the vause of the alarm, the source IP/port and target IP/port associated with the attack, any background relevant to it
      * Post-Processing: process generated alarms, to reduce false positive
      * Security Manager: Stored intrusion signatures are updated by the security manager when a new intrusion become known. The analysis of novel intrusions is highly complex, the security manager has to analyze the alarm data, recognize novel intrusions and update the signature or profile base.
* Unsupervised Anomaly Detection
  * Architecture
    * Unsupervised Engine
      * 2 modules - Detection & Label
      * Detection Module - groups similar instances or identifies exceptional instances
      * Label Module - label the instance as normal or anomalous
    * Labeling Strategy
      * Clustering method simply groups the data without any interpretation. So we need labeling strategies to help interpretate the groups
      * Here are the common assumptions made:
        * The number of normal instances is vastly larger than the number of anomalous instances
          * Exception 1: DoS or DDoS (distributed denial of service) attacks usually generate large number of  similar instances which can be larger than normal instances group
          * Exception 2: R2L (remote to local), U2R (user to root) has similar clusters as normal clusters
        * Anomalies are qualitative difference from normal insatnces
        * Similarity among anomalous instances is higher than similarity among normal instances
        * So we cannot only check cluster size, need to check other cluster characteristics
* Hybrid Detection
  * I uses unsupervised followed by supervised approach, so that unsupervised can only be used for detecting new anomalies
  * Architecture
    * ![hybrid architecture](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/hybrid%20architecture%20of%20ANIDS.png)
    * Supervised Learning is used to detect known attacks, then it will use unsupervised to help detect new attacks. If a new attack has been identified and confirmed, its reference (rule or signature) will be updated and inserted into the rulebase for future use
    * For different dataset, different classifiers will have different performance. It is important to choose the right supervised or unsupervised classifier for the dataset is critical
* Aspects of Netword Anomaly Detection
  * <b>Proximity Measures, Relevant Feature Selection, Anomaly Scores</b>
* Similarity/Proximity Measures
  * [Distance/Similarity Measures between Probability Density Functions][2]
    * It summarized many distance measures
    * PDF (probability dentisy functions) here are related to histograms. Each bin has a count xi, pdf for a bin = xi/n, n is the total count
  * [Outlier Detection Methods in Anomalies Detection][3]
    * Check the methods in 2 tables
    * Some methods are real time
    * [fuzzy set vs rough set][4] - why these researchers cannot user 1 or 2 sentences to summarize the differences...
      * [An easy-to-understand video about fuzzy logic][5]
        * fuzzy set and membership function
      * [Scikit Fuzzy][6]
      * [Scikit Fuzzy Examples][7]
      * [Rough Set Theory used in Anomalies Detection][8]
        * RST is used for dimensional reduction/feature selection here
    * [Kernel based IDS][9]
      * It says it's real time, but more than 1 sec is really too long to be real time...
      * [Kernel PCA][12] is able to find a projection of the data that <b>makes data linearly separable</b>
    * [Anomaly Detection with Supervised & Unsupervised Methods][11]
      * The existing ANIDS systems summary
      * Attack Detection with KDD99 data using Supervised, Unsupervised data. They found that supervised has lower FPR while unsupervised methid is better at detecting unknown methods
* Anomaly Scores
  * Same as [Outlier Detection Methods in Anomalies Detection][3]
* Feature Selection
  * Feature Selection vs Feature Extraction
    * Feature selection selects a subset of features from the original dataset
    * Feature extraction projects original features into another feature space with lower dimension, such as PCA, SVD (singular value decomposition)
    * Both are trying to reduce the dimension
    * Feature Selection Basic Steps
    ![feature selection basic steps](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/feature%20selection%20basic%20steps.png)
    * Heuristic Subset Generation - forward, backward, bidirectional. In most cases, backward and bidirectional may work better than forward
    * Complete Subset Generation - generate all possible subsets of features (pow(2,n) unique subsets)
    * Dependent vs Independent subset evaluation criteria: Dependent criteria is to assess the results of dependent variables created by your model; Independent criteria is just to check features, such as similarity, correlation, etc.
    * Subset Evaluation Measures
    ![Subset Evaluation Measures](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/subset%20evaluation%20measures.png)
* Summarized anomaly detection methods
![anomaly detection methods](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/anomaly%20detection%20methods.png)
* AIS - Artificial Immune System
  * The idea is inspired by human immune system, the way it detects anomalies to protect our health
  * [An overview of AIS][40]
    * <b>It has the pseudo code of somemajor algorithms in AIS</b>, also relevant papers, one did a real-time detection
  * [Artificial immune system based on interval type-2 fuzzy set paradigm][38]
    * [More about type-2 fuzzy sets][39]
* [Fuzzy Association Rules][41]
  * They used basic association rules algorithms to train on normal sample and got fuzzy association ruleset, then for the etsting data, they generate rules and check the compability of generated rules with training data rules, when the compability value is higher than a threshold, label as 'normal', otherwise 'un-normal'
    * Using normal data only as training data, can help detect unknown attacks
  ![association rule classification](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/association%20rules%20prediction.png)
* Markov Chain in Anomaly Detection
  * [Markov Chain Model to seperate normal and intrusive activities][42]
    * It focuses on host intrusion, using audit data
    * Markov is used to build a temporal profile of normal & intrusive activities
      * The probability distribution of the state at time t+1 is dependent on the state at time t, but not dependent on earlier states
      * A state transition from t to t+1 is indenpendent of time
    * They calculated the probability of the support to the testing data from normal activities and intrusive activities, then based on the differences between the probabilities, they said the method can differentiate normal activity and intrisive activity clearly
  * [Hidden Markov Models][43]
    * It's a type of dynamic bayesian network, which means it's a bayesian network model for tiem series data
    * It's represneting the probability distribution over sequences of observations
* [Gausian Mixture Model in Anomaly detection][44]
  * I like this paper, it described the experimental steps, background info and concepts in detail
  * HGMM 2 Phases
  ![HGMM 2 Phases](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/HGMM%202%20phases.png)
  * [PyMC3 - Probabilistic Programming in Python][45]
    * [Model Examples - wow!][46]
    * [IPython practical examples!][47]
* [2 Stage PCA NN][48]
  * I like multiple points in this paper
    * <b>It describes how PCA works well</b>, finally I learned more about the projections
    * Each class of KDD99 data, they used an individual PCA to train in the first stage
    ![2 stage PCA NN](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/2%20stage%20PCA%20NN.png)
    * Among all the evaluation metrics, CPE considers the cost matrix, which represents the cost penalty for misclassifying an instance belonging to class i into class j.
    ![evaluation metrics](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/evaluation%20methods.png)

* Evaluation Methods
![3d evaluation measures](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/3d%20evaluation%20methods.png)
  * Correctness
    * Sensitivity & Specificity
      * `Sensitivity (recall or true positive rate) = TP/(TP + FN)`
      * `Specificity (true negative rate) = TN/(TN + FP)`
      * This method measures how accurate the prediction in both positive & negative classes
    * Misclassification Rate
      * `Misclassification Rate = (FP+FN)/(TP+TN+FN+FP)`
      * It measures the probability of disagreement between true label and the predicted results
    * Confusion Matrix, precision & recall, F1
      * Can be used on n-class prediction
      * `F1 (balanced F score) = 2*precision*recall/(precision+recall)`, with F1, you get a hamonic mean of precision and recall. F1 is a prefered metrics for n-class prediction
    * ROC curve
      * TPR, FPR
      * Sometimes, when comparing 2 models, one model has higher TPR but lower FPR, the other one is the opposite. So better to calcuate AUC at the same time.
    * Cost Matrix & confusion Matrix
      * Measures the cost penality of each dis-classification
  * Data
    * Data Quality
      * Better not to oversampling not under-sampling, better to be balanced to reduce bias (I don't really agree in many cases)
      * The time of data collection, better to be recently updated
    * Data Validity
      * Internal Validity: it measures the degree of certainty that observed effects is in experimental condition, without being affected by other extra factors
      * External Validity: it measures the generic characteristics
    * Reliability (so hard to achieve in many cases)
      * Complete (full observations and variables)
      * Consistent 
      * Kappa Analysis - multiple people analysis, statistical reliability test
  * Efficiency
  
* <b>Attack Launch Tools</b>
  * Overview
  ![attack tools](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/attack%20tools.png)
  * Sniffing Tools
    * "A sniffing tool aims to capture, examine, analyze and visualize pack- ets or frames traversing the network. To support extraction of addi- tional packet features and for subsequent analysis, it also understands the protocols and accordingly includes protocol parameters during vi- sualization."
    ![sniffing tools](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/sniffing%20tools.png)
  * Network Mapping or Scanning Tools
    * "A network scanning tool aims to identify active hosts on a network, either (i) to attack them or (ii) to assess vulnerabilities in the network. It provides an overall status report regarding network hosts, ports, IPs, etc. The four possible types of port scans are (i) one-to-one, (ii) one-to- many, (iii) many-to-one and (iv) many-to-many."
    ![mapping & scanning tools](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/scanning%20tools.png)
  * Attack Launching Tools
    * [Attack Tools 1][49]
    * [Attack Launch Tools 1][50]
    * [Attack Launch Tools 2][50]
  * Packet Forging Tools
    * "Packet forging tools are useful in forging or manipulating packet in- formation. An attacker can generate traffic with manipulated IP ad- dresses based on this category of tools."
    ![packet forging tools](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/packet%20forging%20tools.png)
  * Fingerprinting Attack Tools
    * "Fingerprinting tools are used to identify specific features of a network protocol implementation by analyzing its input and output behavior. The identified features include protocol version, vendor information and configurable parameters. Fingerprinting tools are used to identify the operating system running on a remote machine and can also be used for other purposes."
    ![fingerprinting tools](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/fingerprinting%20tools.png)
  * Other Attack Related Tools
  ![Other Attack Related Tools](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/other%20attack%20tools.png)
  * Monitoring Tools
  ![Monitoriing Tools](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/monitoring%20tools.png)
    
  
* <b>Public Cyber Datasets</b>
  * [KDD][13]: it is an intrusion detection benchmark dataset.
    * [Attack Types1][14]
    * [Attack Types2][15]
  * [NSL-KDD][16]: it is the cleaned version of KDD99, by removing duplicated records and threfore to reduce the bias
    * [Description][17]
  * [Canadian Institution for CyberSecurity][18]
  * [ADFA-IDS-Dataset - Hosted based IDS][19]
  * [PCAP - A list of public packet capture repositories][20]
  * [West Point Cyber Research Center][21]
  * TUIDS dataset - private, here are the main tools they used to collect the data
    * [Gulp][22] captures packets directly from the network and can write to disk at a high rate
    * [Wireshark][23] to analyze the packsts
    * [tcptrace][24] to extract features at packet level traffic
      * [portscan features][26]
      * [flow features 1][27]
      * [flow features 2][28]
* Network Simulation
  * [NS-3 Network Simulator][25]
  
  
## USE CASES

* Supervised Learning in Signature Detection
  * Association Rules
    * With priori knowledge (domain knowledge), you will be able to filter out rule or add constraints to rules
    * Here's an example about how to interprete association rules in signature detection. `confident=1` indicates that all the mail sent has this pattern/satisfy this rule. `support=0.25` indicates that 25% of the instances in the data data has this pattern
    ![assiciation rule in signature detection](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/association_rule_signature_detection.png)
  * Fuzzy-Rule Based
    * Rules in association rules gives an absolute answer for classification, that is the rule leads to this class and not that class. Fuzzy-Rule based method is to give the probability to the rule of which class it belongs to, by comparing the similarity between rules
    * In a word, it's similar to classification problems, we generate Response or Probability as the prediction results
    * [This paper has provided 3 detailed methods about fuzzed-rule based attack detection][54]
  * ANN (Artificial Neural Network)
    * Fast and Accurate
    * But the attack data has to be large enough in the training data, and be balanced as normal data (which in challenging in practice)
  * SVM
    * Faster than ANN - Speed is important in real time detection
    * Scability is better than ANN, which is important in large cyber infrastructure information flow
    * SVM can also DYNAMICALLY update the training patterns, which is important when attack patterns changed
    * SVM works better when the data amount is small but feature count is large
  * Genetic Programming (GP)
    * I think these methods are more related to feature selection and therefore finally you got optimized model/features
    ![GP](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/GP.png)
    * Practical Examples using GP
      * [Feature Selection][56]
      * [Algorithms used in Optimization problems][57]
  * Decision Trees
    * Nonparametric, so it doesn't make assumptions on the data
    * Can help generate rules
    * High prediction accuracy, intuitive knowledge expression, simple implementation, efficiency and strength in handling high dimensional data
    * Entropy vs Gini Index
      * Entropy measures the amount of disorder in a set or how mixed a set is. Higher the entropy is, more mixed th set is. When we are going to choose a feature to split the tree, choose the feature that will lead to lowest entropy
      * How to calculate Entropy
        * `p(i) = count(outcome)/total_records`, it's the frequency of each item
        * `Entropy` start as 0.0
        * `Entropy = Entropy - p(i)*log2(pi) = -sum(p(i)*log2(pi))`
      * [Example to calculate Entropy & Information Gain][58]
      * `Gini Index = 1 - sum(p(i)^2)`
      * [Example to calculate Gini Impurity][59]
      * Compared with Gini Impurity, Entropy peaks slower and tends to penalize mixed sets a little more heaviler.
  * Bayesian Network
    * If rule-based methods tend to consider each individual features seperately, bayesian network will include the dependency between features
    * Naive Bayesian is an exception, it assumes all the features are independent from each other, different from other Bayesian network methods
* Anomalies Detection
  * Association Rules, Fuzzy Rule-based methods
  * ANN
  * SVM
  * KNN - k has to be larger than the number of distinct anomaly type. Distance Based, Density Based
  * Hidden Markov Model (HMM)
    * It can model temporal variations in program behavior. 
    * With HMM, you have a set of normal sequences, when there is a testing sequence, you calculate the similarity probability, lower than a threshold, the testing sequence will be marked as anomaly.
    * I think this method is especially useful when behaviors of a program are happening in time order
    * HMM has high accuracy, but the training time is long because the training requires mutiple passes, it also requires extensive memory to store transition probability through the training.
  * Kalman Filtering
    * It uses a series measurements along the time,instead of only 1 measurement
  * One Class SVM or One Class other algorithm
    * These are unsupervised learning, with these algorithms, you are trying to measure the similarity between training and testing data
    * sklearn has already had the implementation: http://scikit-learn.org/stable/auto_examples/svm/plot_oneclass.html
  * Entropy
    * To make it simple, it measure the change rate of an attribute in network flow. For example, the network under attack tend to have package header with more variety (higher change rate, higher Entropy) 
    
* Graph Database
  * [Neo4j Fraud Detection][55]
    * The basic idea here is, multiple fraudsters are using duplicated entities when do the fraud. Using graph database can help find these links. What makes graph database better is, it generates those links to help you understand the connections between features, instead of just look at each feature seperately. Meanwhile, the connections can give better interpretation of the problem.
    
* Feature Extraction in Malicious Software Installation
  * [Based on Software Name][61]
    * tf-idf of the software name
    * How many spaces the software name has
    * How many vowels (aeiou) the software name has

## HUMAN COMPUTER INTERACTION

* [Mouse Movement, Keystroke Dynamics and User Emotions][1]
  * The sumarized patterns in mouse movent, keystroke and their correlation with user psychological behavior is pretty good
  * Data Collection
  * Data Analysis is major checking correlation between 2 items
* [Biometric Cryptosystem based on Keystroke Dynamics and K medoids][10]
  * It changes single param and check the changes of False Acceptance Rate, False Rejection Rate along the way
  * It uses time sequence, sequencing data
  * But, it raised my question again. Same User vs Different User, and Real User vs Attacker, are they the same?
* [Unconstrained keystroke dynamics][31]
  * They got better results by doing filtering BEFORE selecting into the training data - Samples are added only when they are not far too different from the enrolled samples.
    * The new sample is added to the database only if it is well-correlated with the enrolled samples. 
    * They used absolute value of the Pearson correlation factor between the test vector and the average enrolled vectors.
  * Individual threshold is a little better than global threshold - each individual user will have a accept/reject threshold, instead of using the same thresholds for all the users
    * But it cannot be applied in the case of using a different password for each user
  * There is a small break before typing the next password which can help avoid the problem of users typing mechanically too similar patterns 
  * They have tested if this error rate of acquiring process is dependant on the user’s typing speed, but it seems that there is no significant correlation (The Pearson correla- tion factor between typing speed and acquisition error rate is -0.28).
  * There is no significant difference between the two keyboard during the enrollment and verification phases.
* [Sliding vs Growing window][32]
  * In fact, in this paper, it compared multiple data processing methods, Sliding, Growing, others with Static method
    * Static Method, they used 10 records training
    * Sliding Window: replace the oldest one with the newest qualified one
    * Growing Window: keep growing the qualified records
    * Other methods, looks like will take longer time to process
  * Sliding vs Growing Windows
    * It seems that Sliding window method provides the balanced accuracy close to the best result
    * Sliding window has lower False Accept Rate (accept the different user rate) than Growing window, but has higher False Reject Rate (reject the same user rate) than Growing window
      * I think this finding is very interesting
      * This is true in all the 3 datasets
  * The comparison of 3 datasets here is pretty good
  ![3 datasets](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/3%20datasets.png)
  * It is a better practice to report FAR, FRR with the params
* [Soft biometrics to help prediction][36]
  * It gets help from soft biometrics for more accurate prediction. Soft biometrics such as age, gender, one/two hands typing, left/right hand typing
  * feature vector "[PP, RR, PR, RP]"
  * When using resampling with replacement, they calculated CI (confidence interval) at 95%, `CI = sample_mean * sample_standard_deviation/sqrt(N)`, N = 100 here which means ramdomly draw 100 times
* [Android keystroke dynamics][37]
  * Some of their feature elements are interesting
  ![android features](https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/android%20keystroke%20features.png)
  
* <b>DATASETS</b>
  * [GREYC-keystroke dataset][29]
    * Their dataset is in .db format, that's sqlite files, you need to use [sqlite browser][30] to open the files, then you will see each table in the file. Just click that .db file after installing sqlite browser.
    
## OPEN SOURCES
* [Snort - Rule Based IDS][35]
  * This open-source system matches each packet it observes against a set of rules.
  * Snort rules identify attack packets based on IP addresses, TCP or UDP port numbers, ICMP codes or types and contents of strings in the packet payload.
  * Each Snort rule has associated documentation with the potential for false positives and negatives, together with corrective actions to be taken when the rule raises an alert.
  * An intrusion detection system like Snort can run on a general purpose computer and can try to inspect all packets that go through the network. However, monitoring packets comprehensively in a large net- work is obviously an expensive task since it requires fast inspection on a large number of network interfaces. Many hundreds of rules may have to be matched concurrently, making scaling almost impossible.
* [Anomaly Detection in R][60]


## REFERENCES

* [Network Anomaly Detection:A Machine Learning Perspective][33]
  * [Official Link][34]
  * The book provides details description in all chapters. It's also like a book of survey, instead of describing all the complex concepts, it refered many papers and briefly summarized how those research work with relevant methods.
  
* [Data Mining and Machine Learning in Cybersecurity][52]
  * This book has specific simple use cases, to help you understand how to apply those machine learning methods in cyber security

[1]:https://github.com/hanhanwu/readings/blob/master/Mouse%20behavioral%20patterns%20and%20keystroke%20dynamics%20in%20End-User%20Development.pdf
[2]:https://github.com/hanhanwu/readings/blob/master/distance_similarity_measures.pdf
[3]:https://github.com/hanhanwu/readings/blob/master/A_Survey_of_Outlier_Detection_Methods_in_Network_A.pdf
[4]:https://github.com/hanhanwu/readings/blob/master/fuzzy_vs_rough.pdf
[5]:https://www.youtube.com/watch?v=r804UF8Ia4c
[6]:https://www.youtube.com/watch?v=qUQf1JxnTnY
[7]:http://pythonhosted.org/scikit-fuzzy/auto_examples/index.html
[8]:https://github.com/hanhanwu/readings/blob/master/roughset_anomaly_detection.pdf
[9]:https://github.com/hanhanwu/readings/blob/master/kernel_based_IDS.pdf
[10]:https://github.com/hanhanwu/readings/blob/master/Biometric%20Cryptosystem%20based%20on%20Keystroke%20Dynamics%20and%20K%20medoids.pdf
[11]:https://github.com/hanhanwu/readings/blob/master/Anomaly%20detection%20analysis%20of%20intrusion%20data%20using%20supervised%20and%20unsupervised%20approach.pdf
[12]:http://scikit-learn.org/stable/auto_examples/decomposition/plot_kernel_pca.html
[13]:http://kdd.ics.uci.edu/databases/kddcup99/task.html
[14]:https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/KDD%20attacks1.png
[15]:https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/KDD%20attacks2.png
[16]:https://github.com/defcom17/NSL_KDD
[17]:http://www.unb.ca/cic/datasets/nsl.html
[18]:http://www.unb.ca/cic/datasets/index.html
[19]:https://www.unsw.adfa.edu.au/australian-centre-for-cyber-security/cybersecurity/ADFA-IDS-Datasets/
[20]:http://www.netresec.com/?page=PcapFiles
[21]:https://www.westpoint.edu/crc/SitePages/DataSets.aspx
[22]:http://staff.washington.edu/corey/gulp/
[23]:https://www.wireshark.org/download.html
[24]:http://www.tcptrace.org/download.shtml
[25]:https://www.nsnam.org/overview/what-is-ns-3/
[26]:https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/portscan%20features.png
[27]:https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/flow%20features1.png
[28]:https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/flow%20features2.png
[29]:http://www.epaymentbiometrics.ensicaen.fr/resources/databases
[30]:https://github.com/sqlitebrowser/sqlitebrowser
[31]:https://github.com/hanhanwu/readings/blob/master/Unconstrained%20keystroke%20dynamics.pdf
[32]:https://github.com/hanhanwu/readings/blob/master/sliding%20vs%20growing%20window.pdf
[33]:http://proquest.safaribooksonline.com.proxy.lib.sfu.ca/9781466582095?uicode=simonfraser
[34]:https://www.crcpress.com/Network-Anomaly-Detection-A-Machine-Learning-Perspective/Bhattacharyya-Kalita/p/book/9781466582088
[35]:https://www.snort.org/downloads/#rule-downloads
[36]:https://github.com/hanhanwu/readings/blob/master/profiling%20while%20type%20passwords.pdf
[37]:https://www.sciencedirect.com/science/article/pii/S221201731500119X
[38]:https://github.com/hanhanwu/readings/blob/master/AIS%20anomaly%20detection.pdf
[39]:https://www.iitk.ac.in/eeold/archive/courses/2013/intel-info/d1pdf3.pdf
[40]:https://github.com/hanhanwu/readings/blob/master/ais.pdf
[41]:https://github.com/hanhanwu/readings/blob/master/fuzzy%20association%20rules%20in%20anomaly%20detection.pdf
[42]:https://github.com/hanhanwu/readings/blob/master/markov%20chain%20anomaly%20detection.pdf
[43]:https://github.com/hanhanwu/readings/blob/master/An%20Introduction%20to%20hidden%20Markov%20models%20and%20Bayesian%20networks.pdf
[44]:https://github.com/hanhanwu/readings/blob/master/GMM%20anomaly%20detection.pdf
[45]:http://docs.pymc.io/notebooks/getting_started
[46]:http://docs.pymc.io/examples
[47]:https://hub.mybinder.org/user/pymc-devs-pymc3-vs79j63z/tree//docs/source/notebooks
[48]:https://github.com/hanhanwu/readings/blob/master/2%20stages%20PCA%20NN.pdf
[49]:https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/attack_tools.png
[50]:https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/attack%20launch1.png
[51]:https://github.com/hanhanwu/Hanhan_CyberSecurity_DataScience/blob/master/attack%20launch2.png
[52]:https://dl.acm.org/citation.cfm?id=2018783
[54]:https://pdfs.semanticscholar.org/2a90/534ed66493159991a7e6d400d3854edbfd2a.pdf
[55]:https://github.com/hanhanwu/readings/blob/master/Neo4j_WP-Fraud-Detection-with-Graph-Databases.pdf
[56]:https://www.kaggle.com/randxie/genetic-algorithm-for-feature-selection
[57]:https://github.com/hanhanwu/Hanhan-Machine-Learning-Model-Implementation/blob/master/ReadMe_Optimization.md
[58]:http://www.saedsayad.com/decision_tree.htm
[59]:http://people.revoledu.com/kardi/tutorial/DecisionTree/how-to-measure-impurity.htm
[60]:https://github.com/pridiltal/ctv-AnomalyDetection
[61]:https://www.analyticsvidhya.com/blog/2020/09/machine-learning-in-cyber-security-malicious-software-installation/?utm_source=feedburner&utm_medium=email&utm_campaign=Feed%3A+AnalyticsVidhya+%28Analytics+Vidhya%29
