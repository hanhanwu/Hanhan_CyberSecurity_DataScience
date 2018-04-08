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
  * [PyMC3 - Probabilistic Programming in Python][45]
    * [Model Examples - wow!][46]
    * [IPython practical examples!][47]
  
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

**************************************************************************************************

BIOMETRICS

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
    
**************************************************************************************************
    
OPEN SOURCES

* [Snort - Rule Based IDS][35]
  * This open-source system matches each packet it observes against a set of rules.
  * Snort rules identify attack packets based on IP addresses, TCP or UDP port numbers, ICMP codes or types and contents of strings in the packet payload.
  * Each Snort rule has associated documentation with the potential for false positives and negatives, together with corrective actions to be taken when the rule raises an alert.
  * An intrusion detection system like Snort can run on a general purpose computer and can try to inspect all packets that go through the network. However, monitoring packets comprehensively in a large net- work is obviously an expensive task since it requires fast inspection on a large number of network interfaces. Many hundreds of rules may have to be matched concurrently, making scaling almost impossible.

**************************************************************************************************

REFERENCES

* [Network Anomaly Detection:A Machine Learning Perspective][33]
  * [Official Link][34]
  * The book provides details description in all chapters. It's also like a book of survey, instead of describing all the complex concepts, it refered many papers and briefly summarized how those research work with relevant methods.

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
