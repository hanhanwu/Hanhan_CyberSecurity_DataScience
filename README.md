# Hanhan_CyberSecurity_DataScience
Applied data science in cyber security


**************************************************************************************************

NETWORK ANOMALUES & DATA SCIENCE

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


**************************************************************************************************

BIOMETRICS

* [Mouse Movement, Keystroke Dynamics and User Emotions][1]
  * The sumarized patterns in mouse movent, keystroke and their correlation with user psychological behavior is pretty good
  * Data Collection
  * Data Analysis is major checking correlation between 2 items
* [Biometric Cryptosystem based on Keystroke Dynamics and K medoids][10]
  * It changes single param and check the changes of False Acceptance Rate, False Rejection Rate along the way
  * It uses time sequence, sequencing data
  * But, it raised my question again. Same User vs Different User, and Real User vs Attacker, are they the same? When your mom logins your phone, your computer, her different biometrics should be considered as attacker or different user, and how to dieal with this type of user? I just feel, many researchers confuser the different user and attackers, and there is a gap between real world requirements and the technology here. You build a tool to detect whether this is the same user, but his mom logged in, your tool detect that as different user and will give alarm, how many alarm the system will generate when a non-threaten user logs in....

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
