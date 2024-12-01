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

![image](https://github.com/user-attachments/assets/9b6c295c-7c11-4bb9-834d-37c1b8b035a2)
</br>

This is the basic workflow which we will be working in this project<
</br>
</br>

## Objective
1. Setting up **LimaCharlie**
2. Setting up **Tines** amd **Slack**
3. Writing rules for **LimaCharlie** 
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


## Objective 2: Setting up Tines and Slack
- Setup **Tine** and **Slack.**
- Test our connection between **Tines** and **LimaCharlie.**
- To make sure our **SOAR** is seeing the detection generated by **LimaCharlie.**

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


