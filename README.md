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
  


**************************************************************************************************

BIOMETRICS

* [Mouse Movement, Keystroke Dynamics and User Emotions][1]
  * The sumarized patterns in mouse movent, keystroke and their correlation with user psychological behavior is pretty good
  * Data Collection
  * Data Analysis is major checking correlation between 2 items


[1]:https://github.com/hanhanwu/readings/blob/master/Mouse%20behavioral%20patterns%20and%20keystroke%20dynamics%20in%20End-User%20Development.pdf
