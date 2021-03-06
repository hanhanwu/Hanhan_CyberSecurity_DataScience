This is my very first DEF CON.

## My Overall Feelings
It was such an amazing conference, creative, lively, practical and creepy. Talks related to AI made me feel, it's lucky that my company has much more opportunities to do different experiments & analysis, solving real world problems and finally they will all become products. From other talks not related to AI, I have learned a lot, although got scared along the way... Finally got the cold (I haven't got sick for 2+ years...). Time to take care of myself well. Love the badges most. Oh! It was overcrowded this year, I have never been waiting in lines for such a long time just in order to attend the talks.

## A Boat of Notes
### Aug.9
Today is day 1, most of the villages didn't have any talk yet and therefore all the talks gathered in Flamingo. There were so many people in that giant ballroom, that after each talk, if you want to get to the bathroom, you need to wait in the line and slowly moved out.... Then when you wanted to come back, you also need to wait in line but just could not find the end of the line.... Anyway, among limited amount of talks today, I took the notes and one of them was especially interesting.
* About under surveillance
  * I think this is a sensitive talk and I don't want to expose too much here, although later DEF CON will post videos. This talk is about anyone can be under surveillance and you didn't know. Besides talking a lot about how could you tell you are under surveillance, and how to avoid being under surveillance, they also used fun and impressive videos to show how did UA security agencies track Russian spies.
  * Although I won't put my detailed notes here, the speakers have created an open source to automatically recognize the license plates: https://github.com/openalpr/openalpr

### Aug.10
Today was tired but amazing. I have attended all the talks I was very intereted in, especially those related to data science, and I did learned a lot. Although I was busy with walking between Track2, Track2, Flamingo and Caesars Palace in such a hot weather, with so many people here, often got stuck in the crowd or got lost, finally I was still able to made them all. Sometimes, you just think nothing and keep walking toward that direction, finally you maybe even surprised by yourself.

#### De-anonymizing Programmers from Source Code & Binary
This must be my favorite talk today. The 2 presenters are female professors, and their really did a systematic research, things sounded very clear according to their talk. Other talks all presented by men and I could strongly see the differences, those men tend to present more technical details, but just raised me more questions.
* The major goal of this reasearch is to identify programmers based on their coding style. They were focusing on python and C/C++.
* "stylometry": The style of NLP such as English and Chinese, or the style of artificial language such as Java and Python.
* Part 1 experiments - with lexical features, layout features
  * With Google code jam as data source
    * They have collected 1600 programmers' code, each task is supposed to be finished by individuals. The task has easy and hard levels.
    * Features came from fuzzy AST tree and control flow - lexical features and layout features
    * For binary code (malware author tend to write binary code and hide their identity), they used reverse engineering to disassembly the code and to do decompilation in order to generate AST tree (for extracting lexical features), and to generate graph flow (for extracting control flow features)
      * The dimensional reduction here is interesting:
        * Oringinally they got 700,000 features
        * Then they only kept those features that will reduce entropy (increase purity), now 2000 features left
        * Next they only kept features with lower iter-correlation, so finally 53 features left
    * They majorly used random forest to deal with this multi-class problem, predicting whether a testing code came from the targeting programmer. They got high accuracy (90+% accuracy). They also tried to used open-LLVM to de-anonymized the code, but still they could reach to 80+% accuracy of coder identification.
  * They also tried real world data, from 50 programmers who wrote compilable code in GitHub, and also 6 malicious programemrs from Nulled.io hackers and malware authors.
    * When it comes to GitHub, there can be collaborative code that written by multiple people.
    * They used calibration curve to tell the confidence of their accuracy
    * With 4 samples that have 38+ LOC, they got 54% accuracy; but with 150 samples that has only 1 LOC each, they got 75% accuracy. So the assumption here is, when there are more samples, even less LOC, the accuracy can improve.
* Part 2 experiments - deep learning with new features
  * With deep learning, they didn't used lexical features or layout features used above, but just extract AST features from AST tree. They also tried random forest, LSTM and BiLSTM. Both LSTM outperformed random forest, but without lexical/layour features, the accuracy is a bit lower.
* Future work
  * How much coding style will change when the programming language changed
  * Attributing groups, detecting how much collaboration invloved
    * They have already found thet the more difficult tasks you finished, your coding style is more unique
  * Coding style by country, such as US vs China
    * They found that using nativa language variable naming has already reached to a very high accuracy (90+% accuracy)
* Their open source: https://github.com/calaylin/bda

#### In AI Village
I listened 2 talks in this village since many people were in line outside, I had to go to other talks and I felt it's more basic to me. It seems that people who did these 2 presentations were using their side projects, they are not researchers who need to publish papers. So, it's already good enough for them to do these hands-on projects.
* The speaker was trying to extract the semantic layer from source code in order to compare the similarity between source code
  * Although he mentioned it was semantic, it's in fact majorly using RNN to predict the next word in a sequence.
  * It's char-RNN, using on character based data to predict the sequence.
    * According to the speaker, this is unsupervised learning, no need label data and can generate the sequence.... But even if you check char-RNN author's input data, it still needs labels: https://github.com/karpathy/char-rnn
    * Also, according to the speaker, he got training accuracy which means he used label data
  * In fact his data source was his own code (lots of code), so he does have label data...
  
#### 20 minuts presentations
* Cracking voicemail
  * The github code is going to be posted here: https://github.com/martinvigo/voicemailautomator
    * It will automatically help you compromize the user's voicemail, you will also be allowed to reset the user's password. But don't do any illegal thing with these tools.
  * The presentation was to show how did he crack your voicemail even when your phone is airplane mode.
* dragnet
  * It uses social engineering to allow you do phishing through email, phone, etc. It's a red team tool.
  * Github code: https://github.com/dragnet-org/dragnet
  * The homepage: https://threat.tevora.com/dragnet/
  
#### Weaponizing Unicode: Homographs Beyond IDNS
* It mentioned to crack machine learning systems in the description, but in fact during the whole talk, it just mentioned machine learning system once and not really relevant.
* Majorly it's about social engineering can use unicode to create lines that looks like the letters but in fact not

#### Your Voice is My Passport
They were using machine learning to change the speaker's voice with target voice
* Getting Youtube raw data -> Subsample high quality data (may lead to overfitting, as they admitted) -> Data Augmentation, Pitch Shift, using pytub -> Transfer Learning, they trained the model with larger data from Blizzard, then replace the data source with targeting data -> finally they could change the voice
* Attacks on ML system
  * Adversarial Attack; Posining the Well: all try to poisoning the training data to lead to misclassification
  * Differential Privacy
* Attacks with ML System
  * Phishing
  * Deepfakes (they said currently majorly used in porn websits)
  * Social Engineering
    * Yeah, the attacker can mimic someone's voice to communicate with you....
* Speak Recognition: weak signal for authentication
* Speak Authentication: can be broken if the attacker knows the target voice data and authentication prompt

#### Your Bank's Digital Side Door
* It tells you Personal Financial Management has poor architecture, banks are still using out of dated 2 factor authentication and none of these are safe to your money.

### Aug.11
What to say about today. It was very tired to get up as usual because of the busy schedule yesterday and I had to walk fast across the crowds. Today, besides feeling very tired, I also got scared in multiple talks.

#### Guide to Adversarial Testing of the Software used in Criminal Justice Systems
* You can find all of their GitHub here: https://github.com/propublica
* The talk today is about the Adversarial Testing of software used in Criminal Justice System. Software all has bugs, but imagine if everything the software tells you will be considered as the truth or the evidence, and you will be put into the prison, are you going to be scared? Their GitHub: https://github.com/propublica/nyc-dna-software

#### Assess the devices used by police
* Scary, because those devices used by the police have too much security issues and too easy to be attacked. Think about this, when those devices got attacked, it's all about citizens' data drop into attackers' hands.
* Details I don't want to write here, those issues really make people jaw dropped.
* According to the speaker, this is his GitHub: https://github.com/bx-lr

#### Looking for the perfect signature, an automatic YARA rules generation algorithm in AI-era
* This one is trying to find malware signature by finding optimal attribute subsets, I didn't really hear much about AI.
* The speaker looks like Emmanuel (I was sitting far away from the stage, btw): https://github.com/jimmy-sonny
* The project is yayagen: https://github.com/jimmy-sonny/YaYaGen

#### Detecting Blue Team Recon with Ads
* Sometimes, blue teams will create Google ad bids, so that when users searched some relevant keywords, they will click the link generated by the blue team.
* However, google is tracking everything. When you are creating an ad, a certain keyword may raise their suspicion. So the speaker was trying to tell blue teams, that be careful to choose your keywords, everything you are doing is tracked.

#### Hacking Hospital Central Monitoring System
* The hospital Central Monitoring System can help doctors to track patients' heart beating rate at their offices.
* But this system is very easy to be comprimized. Currently, it's connecting to the internet and it will consider whatever packages from the patient's IP as the patient... So they demoed in the talk, to show how did they sent the system a package with fake patient's data and changed what's shown there about heart beating rate...
* Suggested Mitigations
  * Encription
  * Authentication
  * Isolated network
    * Network access control - make the network isolated from the internet
    * Physical access control
    
#### The Road to Resilience: How Real Hacking Redeems this Damnable Profession
Keynote speaker is keynote speaker. They can really hold everyone's attention, no matter what they are talking about.
The whole talk was not about technical details, but all about stories that CIA officiers, especially those who quite the job or committed suicide. It seesm that they knew those things and had to keep the security, finally reached to a certain point that they could not stand any more, and therefore the speaker hope we all have a community to make people all feel stronger sense of belongs.
* I agree

### Aug.12
Today is the last day of DEF CON, I'm so tired. I went to all the AI or biometrics related talks, but all got disappointed. Their results are all supervised learning, with very small amount of dataset, methods are also too academeic, which means what they need could only used for publishing papers, not for solving industry prblems. But what I'm looking for, are the inspiations that can make industry solutions better.
* Adversarial Machine Learning
  * It's an area that adapts machine learning in computer security, such as malware detection, spam filtering and biometrics detection.
  * Cannot say I like that talk, and when she was doing the presentation, I'm taking notes about what we need to be careful when we are presenting to a wide variety audience
    * Tell the audience not only the data source, but also need to show them the sample of data input & output
    * Make sure when you are talking about the models, it's understandable to those who never used machine learning before
    * Visualization should show how effective your solution solved the problem.
      * In her talk, she was using T-SNE to show multiple classes. But T-SNE cannot help you really do the classification. If you really like visualization, better to visualize both observed classes and predicted classes through T-SNE, and compare, also make sure the dots are transparent

* Another talk is about how your typing give you away
  * But they only had 10 people as data input.... although each person spent 133 mins on average. 10 people are not representative in real world situation...
  * But he mentioned, fraudsters tend to have consistent fraudluent behaviors that's different from normal people
  
* Intelligent Anti-Malware for Android
  * Their GitHub: https://github.com/IntelliAV
  * Their website: http://intelliav.com/
  
* Other talks, disclosed the problems that haven't been fixed in our current OS... creepy, but what can I do.... I'm too tired. don't want to write them down anymore.


## Before DEF CON - Preparation
This will be my first DEF CON. I booked the flight and hotel at the end of last year, because of the discounts. I'm very excited about it, and also need to be very careful to everything. My own security is the most important.

### What to Remember
* <b>Don't bring any electronic device. Don't bring bank cards but just cash.</b>
* <b>Be careful to whom to talk to.</b>
  * I don't want to be part of someone's research paper, and would there be someone even worse?
* <b>About Identity</b>
  * Level 1 Info: Hotel; Transfortation; Residency
  * Level 2 Info: Name, Company, Job Title, Interest Area
  * <b>Be careful when to give business card</b>
* <b>About the party</b>
  * Check whether it's safe to attend the party. Don't take any risk.
  
### Workshops
* I just found that the workshop needs registration and it opened 1 month ago, only gave a very short time to register, so right now I can no longer register any. But let me take notes about those I'm interested in, just in case there will be a chance.
* All workshops: https://www.defcon.org/html/defcon-26/dc-26-workshops.html
* Pentesting ICS 101
  * <b>Aug. 9, 10am - 2pm</b>
  * 1000-1400 in Icon B
* Hacking Thingz Powered By Machine Learning
  * <b>Aug. 10, 2:30pm - 6:30pm</b>
  * 1430-1830 in Icon A
* Penetration Testing Environments: Client & Test Security
  * <b>Aug. 10, 2:30pm - 6:30pm</b>
  * 1430-1830 in Icon E
  
### Talks
* All the talks: https://www.defcon.org/html/defcon-26/dc-26-schedule.html
#### Aug. 9
* It seems that all the talks are all in Flamingo, so I can just get there early, find a seat and sit there whole day...
* Starting from 10am
#### Aug. 10
* De-anonymizing Programmers from Source Code and Binaries
  * 10am, Track 2
* One-liners to Rule Them All
  * 11am, Track 2
* NSA Talks Cybersecurity
  * 11am, Track 1
* Breaking Parser Logic: Take Your Path Normalization Off and Pop 0days Out!
  * 12pm, Track 2
* Compromising online accounts by cracking voicemail systems
  * 1pm, Track 1
* Dragnet—Your Social Engineering Sidekick
  * 1:30pm, Track 1
* 4G—Who is paying your cellular phone bill?
  * 2pm, Track 2
* Weaponizing Unicode: Homographs Beyond IDNs
  * 3pm, Flamingo
* Your Voice is My Passport
  * 4pm, Track 3
* Your Bank's Digital Side Door
  * 5pm, Flamingo
#### Aug. 11
* You're just complaining because you're guilty: A DEF CON Guide to Adversarial Testing of Software Used In the Criminal Justice System
  * 10am, Track 2
* Jailbreaking the 3DS through 7 years of hardening
  * 11am, Track 3
* Building Absurd Christmas Light Shows
  * 12pm, 101 Track
* Looking for the perfect signature: an automatic YARA rules generation algorithm in the AI-era
  * 1pm, Track 3
* Detecting Blue Team Research Through Targeted Ads
  * 1:30pm, Track 2
* Fire & Ice: Making and Breaking macOS Firewalls
  * 2:30pm, Track 3
* All your math are belong to us
  * 3pm, Track 1
* All your family secrets belong to us—Worrisome security issues in tracker apps
  * 4pm, Track 2
* The Road to Resilience: How Real Hacking Redeems this Damnable Profession
  * 5pm, Track 1
#### Aug. 12
* The Mouse is Mightier than the Sword
  * 10am, Flamingo
* Politics and the Surveillance State. The story of a young politician's successful efforts to fight surveillance and pass the nation's strongest privacy bills
  * 11am, Track 2
* Last mile authentication problem: Exploiting the missing link in end-to-end secure communication
  * 12pm, Track 1
* Trouble in the tubes: How internet routing security breaks down and how you can do it at home
  * 1pm, Flamingo
* Betrayed by the keyboard: How what you type can give you away
  * 2pm, Flamingo
* Fuzzing Malware For Fun & Profit. Applying Coverage-guided Fuzzing to Find and Exploit Bugs in Modern Malware
  * 3pm, Track 3
* DEF CON Closing Ceremonies
  * 4pm, Track 1
