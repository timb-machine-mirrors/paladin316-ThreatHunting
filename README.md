# ThreatHunting
This repo is where I store my Threat Hunting ideas/content

Below are the use cases and file descriptions for the items in this repo:

Before going into what the files are, I will describe my lab setup:

**Lab Ingredients:**

1. Win10 Guest VM configured with Olaf Hartong's sysmon-modular (https://github.com/olafhartong/sysmon-modular)
2. Splunk Enterpirse Evaluation https://www.splunk.com/en_us/download/splunk-enterprise.html installed on Host Linux System
3. Atomic Red Team script to generate the data (https://github.com/redcanaryco/invoke-atomicredteam)



**Use Cases:**

Splunk queries are designed to score LOLBINs activity using a scoring method that bubbles up the most egregious activity to the top of the list based on MITRE techniques. The Scoring model uses four numbers to represent the level of seriousness of the activity seen. The sum of all of the activity is added together to create a total score for each of the MITRE techniques, then added together to create an overall score for each system. Before implementing the scoring system its a good idea is to perform some frequency analysis on LOLBINs usage within your environment. Build out the scoring model according to what you know about your environment (Priciple: Know You Environment). This scoring model will be unique to your environment since no two companies are the same. 


**Scoring Model (Base):**

Base score + Each MITRE Technique Score = Overal Score
1  = (Low) LOLBINs activity that is frequent in the your environment and may be used by some of your Server and Workdstation Support Teams

4  = (Med) LOLBINs activity that is less frequent in the your environment and may be used by some of your Server and Workdstation Support Teams

7  = (High) LOLBINs activity is not frequent in the your environment and may be used by some of your Server and Workdstation Support Teams

10 = (Critical) LOLBINs activity should never be seen in the your environment and is not used by your Server and Workdstation Support Teams


**Scoring Model with Threat Count:**

Base score + Each MITRE Technique Score X The number of occurences for each event = Overal Score 


**Filename & Descriptions:**

1. **Filename**: splunk_sysmon_lolbins_hunt_base_score.txt 
   
   **Description**: Splunk query designed to use the Base Scoring Model to identify suspicious acitivty and diplays details of activity
   
   Examples:
   ![image](https://user-images.githubusercontent.com/15706462/146420453-7faa56cb-bb63-4cb5-8420-84faab6f272d.png)
   [Example_Data-splunk_sysmon_lolbins_hunt_base_score.csv](https://github.com/paladin316/ThreatHunting/files/7729326/Example_Data-splunk_sysmon_lolbins_hunt_base_score.csv)


   
2. **Filename**: splunk_sysmon_lolbins_hunt_base_score_stats_by_computername.txt 
   
   **Description**: Splunk query using the Base Scoring Model to identify suspicious acitivty; **stats only by ComputerName**
   
   Examples:
   ![image](https://user-images.githubusercontent.com/15706462/146420981-c8a69bca-7fa1-489d-a2c8-3c1bd93c9840.png)
   [Example_Data-splunk_sysmon_lolbins_hunt_base_score_stats_by_computername.csv](https://github.com/paladin316/ThreatHunting/files/7729348/Example_Data-splunk_sysmon_lolbins_hunt_base_score_stats_by_computername.csv)


   
3. **Filename**: splunk_sysmon_lolbins_hunt_with_threat-count.txt
   
   **Description**: Splunk query designed to use the Threat Count Scoring Model to identify suspicious acitivty and diplays details of activity
   
   Examples:
   ![image](https://user-images.githubusercontent.com/15706462/146421587-1bcb993d-2676-4ce8-9214-275eece26eed.png)
   [Example_Data-splunk_sysmon_lolbins_hunt_with_threat-count.csv](https://github.com/paladin316/ThreatHunting/files/7729364/Example_Data-splunk_sysmon_lolbins_hunt_with_threat-count.csv)


   
4. **Filename**: splunk_sysmon_lolbins_hunt_with_threat-count_stats_by_computername.txt
   
   **Description**: Splunk query using the Threat Count Scoring Model to identify suspicious acitivty; **stats only by ComputerName**
   
   Examples:
   ![image](https://user-images.githubusercontent.com/15706462/146422029-1f16a1f0-cb6b-428d-8795-a87f5edfdf49.png)
   [Example_Data-splunk_sysmon_lolbins_hunt_with_threat-count_stats_by_computername.csv](https://github.com/paladin316/ThreatHunting/files/7729414/Example_Data-splunk_sysmon_lolbins_hunt_with_threat-count_stats_by_computername.csv)


   
5. **Filename**: splunk_sysmon_lolbins_hunt_with_threat-count_renamed_binaries.txt
   
   **Description**: Splunk query designed to identify renamed binaries and score the activity using the Threat Count Scoring Model
   
   Examples:
   ![image](https://user-images.githubusercontent.com/15706462/146422780-0dfd0833-bbab-4726-9627-cba696dc86e5.png)
   [Example_Data-splunk_sysmon_lolbins_hunt_with_threat-count_renamed_binaries.csv](https://github.com/paladin316/ThreatHunting/files/7729429/Example_Data-splunk_sysmon_lolbins_hunt_with_threat-count_renamed_binaries.csv)



