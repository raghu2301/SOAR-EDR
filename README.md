# SOAR-EDR
## Overview
**SOAR (Security Orchestration, Automation, and Response)** and **EDR (Endpoint Detection and Response)** are two critical technologies in modern cybersecurity, working together to detect, respond to, and mitigate threats effectively.
</br>
</br>
## SOAR: Security Orchestration, Automation, and Response

SOAR platforms are designed to help organizations manage and respond to security threats through a combination of orchestration, automation, and human-driven processes.

**Key Components of SOAR:**
1. **Orchestration:** Integration of various security tools and systems to streamline data sharing and workflows. SOAR centralizes information from diverse sources like firewalls, SIEM (Security Information and Event Management) tools, and EDR solutions.
2. **Automation:** Reduces the manual workload of security teams by automating repetitive tasks, such as alert triaging, threat intelligence gathering, and incident prioritization.
3. **Response:** Provides tools and playbooks to help teams respond to incidents more effectively and consistently, with detailed guidance for decision-making.

**Benefits:**
- Faster threat response times.
- Reduced manual workload for security analysts.
- Improved efficiency and consistency in incident management.
- Enhanced threat visibility by correlating data from multiple sources.
</br>
</br>

## EDR: Endpoint Detection and Response

EDR solutions focus on monitoring and securing endpoints, such as workstations, servers, and mobile devices. These tools provide continuous endpoint visibility, detecting and responding to advanced threats.

**Key Features of EDR:**
1.	**Endpoint Monitoring:** Continuous collection of data from endpoints for suspicious activity.
2.	**Threat Detection:** Uses advanced analytics, machine learning, and behavior-based detection to identify threats like malware, ransomware, and advanced persistent threats (APTs).
3.	**Incident Response:** Enables security teams to isolate compromised endpoints, perform forensic analysis, and remediate threats.
4.	**Integration:** Often integrates with broader security ecosystems, including SOAR and SIEM platforms, for enhanced functionality.


**Benefits:**
- Rapid identification and containment of endpoint-based threats.
- Detailed forensic insights for post-incident analysis.
- Protection against zero-day and fileless attacks.
- Real-time visibility into endpoint activity.
</br>

## Synergy Between SOAR and EDR

While EDR excels at monitoring and securing endpoints, SOAR provides the orchestration layer to bring endpoint data together with broader security intelligence. By integrating EDR into a SOAR platform, organizations can:

1.	**Streamline Incident Response:** Automatically trigger response playbooks based on EDR alerts, reducing response times.
2.	**Enhance Threat Intelligence:** Combine endpoint data with network, cloud, and threat intelligence feeds for a comprehensive security posture.
3.	**Automate Routine Tasks:** Use SOAR to automate actions like quarantining infected endpoints detected by EDR.
4.	**Improve Analyst Efficiency:** Correlate endpoint data with other security events to provide context and prioritize critical threats.
</br>

## Workflow
</br>

![image](https://github.com/user-attachments/assets/97f52ddd-7900-483e-ae61-4415e3a45871)

</br>

This is the basic workflow which we will be working in this project<
</br>
</br>

## Objective
1. Setting up **LimaCharlie**
2. Writing rules for **LimaCharlie**
3. Setting up **Tines** amd **Slack**
4. Creating a **Playbook** and its **Automation**
</br>
</br>

## Objective 1: Setting up LimaCharlie

- Install and setup LimaCharlie.
- Confirm Event end point is connected and generate events.
- one system reporting back to LimaCharlie.
</br>

**Installation**

1. Goto LimaCharlie [website]( https://limacharlie.io/) 
![image](https://github.com/user-attachments/assets/b4d85cd3-a333-43fd-888c-4ce39ab23374)
</br>

2. Click on **Log In** and sign up

![image](https://github.com/user-attachments/assets/9ba37dd7-f638-48ec-8f33-15056f283e1f)
</br>
</br>

3. After Log In **Create Organization**

![image](https://github.com/user-attachments/assets/e023367b-79ae-49b7-966b-cd81861f8f0e)


On sensor tab only 2 tabs we need to focus on is sensor list and installation key.
- **Installation Key** is what is going to be used to enroll your machine to LimaCharlie.
- **Sensor list** will then contain your machine once it is successfully enrolled
</br>

4. Goto installation keys and Create installation key


![image](https://github.com/user-attachments/assets/39bd56ec-1cf9-4d9a-a376-2abf3eb17ce4)

</br>

5. Scroll down and download the EDR for your system 

![image](https://github.com/user-attachments/assets/4ac563a0-5244-41cd-b65e-d9b3e30a2c9c)

</br>

6. Copy the sensor key

![image](https://github.com/user-attachments/assets/7742964a-51f2-4df0-8be6-34330bc18e90)

</br>
</br>

7. Open powershell as administrator
  change the directory to Downloads
```
cd Downloads
```

```
dir
```
to view the name of the Limacharlie executable

```
hcp <LimaCharlie.exe> -I <paste installation key>
```
replace **LimaCharlie.exe** with the name of executable file.

![image](https://github.com/user-attachments/assets/d9f3376a-3fa8-4ae7-80ed-439577934188)

</br>

8. Goto **Sensor List** your system will be available there
Click it to see more details

 ![image](https://github.com/user-attachments/assets/c4ccb573-927b-4ab2-af41-6b699d15a565)
</br>
</br>


## Objective 2: Writing rules for LimaCharlie
1. Generate telemetryon host machine using **lazagne**
2. Create detection and response rule.
   (Which we can send to tines for automation.)



- Goto [lagaZagne github page](https://github.com/AlessandroZ/LaZagne)
- Click on releases
![image](https://github.com/user-attachments/assets/0f8bfb00-0c2e-4313-86e0-627d37ed772b)

- Disable windows security
  Win security > Manage setting (virus and threat protection) > Disable real time protection
- Download laZane.exe from the github page.
- Goto Downloads folder
- And open powershell
- Run laZagnia.exe
```
.\laZagne.exe
```

![image](https://github.com/user-attachments/assets/0cc1a907-021c-42e9-ac43-e2de1274a24b)

- Since we have run **laZagne** on our host, **LimaChalie** should have picked it up.
- Lets head to **LimaCharlie**
- Select **Sensor list**
- Select the **sensor** (host)
- Select **Timeline**
- Search **laZagne**
![image](https://github.com/user-attachments/assets/b56b159f-fa6c-4b24-805d-778d74afd931)

 It has many information, which will be useful in generating a detection the rule.
![image](https://github.com/user-attachments/assets/254f1c96-a788-46bb-81c1-a9c13c76f385)


- Open a new tab
- Select our organization > Automation > D&R Rules > Create custom Rule
![image](https://github.com/user-attachments/assets/e2b32e59-088f-4327-8322-a50e1a7ccef0)

We don’t need to build a rule from scrath.
- Goto github and find the [code](https://github.com/refractionPOINT/rules/blob/master/Sigma/dr_rules/windows_process_creation/win_process_creation_bitsadmin_download.yml)
- Click on RAW and copy the rules.
![image](https://github.com/user-attachments/assets/90a9623e-c859-4812-9a32-49c80b46ceb9)

- Head back to the rules.
- Create a new rule and paste it.
![image](https://github.com/user-attachments/assets/90a556a2-b308-440f-ae75-b86438e60cc4)

- We can see a **detect** and **respond** section in what we have copied.
  This essentially signifies two blocks.
  Starting from **respond** select all the text and cut paste it to the **respond** block.
![image](https://github.com/user-attachments/assets/4056c1cf-b088-4078-997b-b389c0414d3c)

Remove  the text **respond** from **respond block** and **detect** from **detect block.**
As it is just to specify the blocks.

![image](https://github.com/user-attachments/assets/3d3d290a-7b2c-4f86-b121-7fcaabdd37ae)

Here:
**event:** specifies the event type, this process will only trigger if there is a new process or existing process.
**op:** specifies operator type here. 
It means the event type must be new process or existing process.
rules is going to the criteria this means we must follow the rules.
Op: is windows
Case sensitive is false
op is ends with (it is using 2 operators)
path   event/FILE_PATH
value lazagne.

![image](https://github.com/user-attachments/assets/03e0981b-3f66-4f89-83b1-c4e210f97593)

Here is the rule created for **detect** section
```
 events:
  - NEW_PROCESS
  - EXISTING_PROCESS
  op: and
  rules:
  - op: is windows
  - op: and
    rules:
    - case sensitive: false
      op: ends with
      path: event/FILE_PATH
      value: lazagne.exe
    - case sensitive: false
      op: ends with
      path: event/COMMAND_LINE
      value: all
    - case sensitive: false
      op: contains
      path: event/COMMAND_LINE
      value: lazagne
    - case sesitive: false
      op: is
      path: event/HASH
      value: '1c84c8632c5269f24876ed9f49fa810b49f77e1e92e8918fc164c34b020f9a94'

```
![image](https://github.com/user-attachments/assets/13d0711b-96f5-4360-b72c-5865128ac3a9)


Rule for **respond** section
```
- action: report
  metadata:
    author: raghu2301
    description: Detects lazagne (SOAR-EDR-TOOL)
    level: medium
    tags:
    - attack.credential_access
  name: raghu2301 - hacktool - Lazagne (SOAR-EDR)

```

The best thing of **LimaCharlie** is that we can test the configuration.

Copy the event by clicking on copy event
![image](https://github.com/user-attachments/assets/bca7845e-75b0-4a45-b589-5fdeece72495)

Scroll down and goto target event

<img width="569" alt="image" src="https://github.com/user-attachments/assets/fdf7196a-6936-424d-87d0-c7d8cd568ba0">

Paste the copied event, and click on test event.
![image](https://github.com/user-attachments/assets/9bee29ed-2513-43ff-9028-246558192420)

Goto detection.
Here we can see our events generated.
![image](https://github.com/user-attachments/assets/ad847bad-3818-45b4-8a82-ceab3c900c68)

</br>
</br>

## Objective 3: Setting up Tines and Slack
1. Setup **Tine** and **Slack.**
2. Establishing connection between **LimaCharlie, Tines and Slack**
3. Test our connection between **Tines** and **LimaCharlie.**
4. To make sure our **SOAR** is seeing the detection generated by **LimaCharlie.**

**Slack Setup**
- Goto [Slack website]( https://slack.com/intl/en-in)
- Click on **Get Started**
- Signup
![image](https://github.com/user-attachments/assets/0fe40272-557e-46da-9a70-810de5269550)

- Click on **Create a workspace**
![image](https://github.com/user-attachments/assets/7fdfec15-b76c-4239-866e-f821a2fe7b86)

- Fill the name
![image](https://github.com/user-attachments/assets/d9452e0b-5204-44ee-b123-05b70100f79e)

- Add the emails of your colleagues who are in your team or you can skip if you dont want to add anyone
![image](https://github.com/user-attachments/assets/50d89630-dc86-44a0-9caa-a3fd8f93024e)

- Name the project you are working on
![image](https://github.com/user-attachments/assets/445dd01b-00aa-4bed-bf1c-a1fe1e07705d)

- Click on **Start with free**
![image](https://github.com/user-attachments/assets/71223f74-4541-4a3b-a888-5a597c7077dd)

- Create a new channel
![image](https://github.com/user-attachments/assets/545d6d7a-2fca-4bc0-a20a-9d5257d6daec)

- Choose the visibility of your channel
![image](https://github.com/user-attachments/assets/3295e028-8e4e-48bd-a73c-46da5e99030f)

![image](https://github.com/user-attachments/assets/2b7e1d93-03cb-437e-b559-8df99573a15e)
On left side we have a channel called alerts which I have created.
When we receive a detection from **LimaCharlie** on **Tines**. **Tines** will then send a message to **Slack** specifically within the alerts channel. Because as a **SOC Analyst** we would want to have a different channel and we want to have a dedicated channel for our alerts.

**Setting up Tines**
- Headover to [Tines website](https://www.tines.com/)
- Sign up if you are using it for first time
![image](https://github.com/user-attachments/assets/e7bfc6ea-0974-44e4-be60-b8cd9c813171)

- Click on Tines icon and create a New Story by clicking on **New**
<img width="959" alt="image" src="https://github.com/user-attachments/assets/8476f791-a61b-40d6-b3bf-78a35ac9e722">


**Establishing connection**
Establish a link between **LimaCharlie** and **Tines** So that we can know **Tines** is retrieving the detection
For that we will be using **webhook**
**In Tines**
- Click and drag **Webhook** from the left side to the story board
- Copy the **Webhook url**
![image](https://github.com/user-attachments/assets/1e9c8f36-52d2-46fa-95f5-890f761eb97f)

**In LimaCharlie**
- Goto outputs

![image](https://github.com/user-attachments/assets/ec0b47e8-0604-4bba-8ae4-8496385b97fd)

- Add output
![image](https://github.com/user-attachments/assets/c9977f9e-50b3-4dc4-84fe-e1154b8eb594)

There are lot of option like events, detection, deployment etc.
- We are interested in detection.
![image](https://github.com/user-attachments/assets/75dda903-e387-48aa-96b9-f7dc6fc90715)

- Select **Tines**
![image](https://github.com/user-attachments/assets/02c3c2e0-ae93-4ded-a9f7-f304dd5470df)

- Name it and paste the link of the webhook on destination host and save output.

![image](https://github.com/user-attachments/assets/6894e1d3-de38-46d6-bf09-259d71669bd1)

Our configuration is complete.

**Move to Tines**
- Select **Webhook**
- Click on **Events**
![image](https://github.com/user-attachments/assets/29618191-b5f6-43da-ade3-8cb0e521f66b)

Select the recent event and expand the body. We have our detection exactly one to one as **LimaCharlie**

![image](https://github.com/user-attachments/assets/4103088f-07b1-409e-b7f2-ddc41bdb975f)

</br>
</br>

## Objective 4: Creating a **Playbook** and its **Automation**

**Playbook Objective**
- Send a message to **Slack**
- Send a **email**
  (**email** will contain information about the detection that the LimaCharlie has generated)

- Generate a prompt:
  It will contain a message **Isolate the machine(yes/no)**
  If we select **yes** then **LimaCharlie** should automatically isolate the machine.

  
