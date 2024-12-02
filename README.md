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

  In the workflow
  ![image](https://github.com/user-attachments/assets/92ff2912-0c49-4ff6-9c05-33e1b8f114e2)

We have the infected host with the detect hack tool that **LimaCharlie** has detected.
Which is pushed to **Tines.**
**Tines** is going to send a message to **Slack.** This means there should be a link between **Tines** and **Slack.**


To create a link between **Tines** and **Slack**
Goto **Slack** and look at the applications there.
More > Automation > Search **Tines**
![image](https://github.com/user-attachments/assets/d9d95fb8-e93f-444a-aed3-080845444345)

Click on add
![image](https://github.com/user-attachments/assets/687bca2c-2c70-4dfc-872e-dc0a1baafc5c)

Follow the steps mentioned.
![image](https://github.com/user-attachments/assets/b3e4ac0c-b592-4981-8276-715416ef0383)


On **Tines**
Click on Credentials and select Slack
![image](https://github.com/user-attachments/assets/ed09142d-9c6e-4e93-8cb6-6fb7e61f84b8)

Click on **use tines app for slack.** and click on allow
![image](https://github.com/user-attachments/assets/ab777095-2f03-48cb-8595-1ef032380102)

Goto templets and drag **Slack** into the storyboard.
![image](https://github.com/user-attachments/assets/55b0c373-bf37-49e3-89ac-04eb3b97f9d1)

On right side search for message.
And select **send a message.**
![image](https://github.com/user-attachments/assets/395a2055-4437-4b18-acbf-1340ec3f8509)


On **Slack**
- Goto **alert** channel, which we have created.
- Right Click on channel and select **View channel details**
![image](https://github.com/user-attachments/assets/24f93de0-5040-4312-8800-9483956251e0)

- Scroll down and copy the **Channel ID**
<img width="652" alt="image" src="https://github.com/user-attachments/assets/14ee0b6b-1916-496c-a907-d87e4de21d93">

Move to **Tines**
And paste the **Channel/User ID**
![image](https://github.com/user-attachments/assets/bd6bdc27-4eff-47d1-9fdd-65057fe9ef54)

And type the message you want to send.

Now connect the **Webhook** to **Slack**
And click on **Test**

![image](https://github.com/user-attachments/assets/06c530e8-b1aa-4b07-be75-0909093ddf40)

Now got to **Slack** and see the message
![image](https://github.com/user-attachments/assets/42067678-b3f2-4c46-976d-60a183da5950)

The message is visible in **Slack**
Now we are sure that **Tines** can communicate with **Slack.**
</br>
</br>
</br>
Now we need to send a **email.**
Select **email** and drag it to the storyboard.

![image](https://github.com/user-attachments/assets/2567ac72-0391-493d-946a-8d2815533e19)

Connect the **Webhook** to **Send email.**
For testing I will be using temp mail.
Enter email in **Recipients** and **Reply to**
Click on **Test**
![image](https://github.com/user-attachments/assets/108c097c-78d2-465a-83fa-ffd97a65580f)

Goto mail and check the mail.
![image](https://github.com/user-attachments/assets/6392bf69-1a13-4f39-86d0-99c340d8400d)
</br>
</br>
</br>
Now we have to create a **Prompt** as per our workflow.
For **Prompt** we can use **page** which is under tools.
Drag **page** to the storyboard.
![image](https://github.com/user-attachments/assets/2ce74cb9-0705-4e00-9152-90189c35d8a1)


Click on **Edit page.**
Lets include the details into the our messages.
For interesting fields we will goto our **Webhook.**
And expand detection > body

![image](https://github.com/user-attachments/assets/0a309b6f-b297-44cb-8dc3-7f26c2729724)

Open notepad.
Copy and paste the interesting fields.

![image](https://github.com/user-attachments/assets/a045044f-8a4a-4afc-9914-28bc78606fa6)
</br>
</br>
Rearrange the fields according to needs.

Copy the data and paste it on the message.
</br>
![image](https://github.com/user-attachments/assets/7fdb466b-1a5e-4691-84ba-adafa387c43e)

Select the **page** and click on **Test**

**Move to Slack**
We can see the message with all the details included.

![image](https://github.com/user-attachments/assets/b2d37935-4657-456f-8cc2-a556bf256269)

These details are only know to us, but it is not know to others, so lets make it more user friendly.

So we go to our **notepad** again and add the description before the links.

![image](https://github.com/user-attachments/assets/54b3f31a-33d1-4801-ab2c-b406d311f1fa)


Copy this and paste it again on the message, and replace the message which we had earlier.

![image](https://github.com/user-attachments/assets/decafa67-bede-4326-8276-e49b04643fef)

Now we test it again.

Move to Slack.

Updated message will appear.

This time the details have descriptions. So that everyone can understand.
![image](https://github.com/user-attachments/assets/4c5ce8b2-0ba2-44a0-bd61-33d10dac9276)

</br>
</br>
</br>

**Setting the email**
Now we need to send a **email** with these informations.
Click on the **email** we created on the storyboard.
Copy the details we have on the notepad and paste the message to the **body** of the email
Select the mail and press the **Test**
![image](https://github.com/user-attachments/assets/6b86fa08-753f-4c33-bc65-d7d16c75e40c)

Goto the **email** and check the mail.
![image](https://github.com/user-attachments/assets/5368daa9-75b3-445c-93a0-1ac37c0f2adf)

We got the mail, but the formatting is not good.

So we open the html editor of the messages and make changes to break the line.
![image](https://github.com/user-attachments/assets/fbb48fc7-64d1-43b2-8faf-e96b960d9ad7)

And **test** the email again.
And check the mail again.
Now it looks good.
![image](https://github.com/user-attachments/assets/47cc2866-577a-4058-9e14-af5652513eac)

</br>
</br>
<br>

**User Prompt**
Now we have to work on our user prompt.
Does the user want to isolate the pc.

Select user prompt and edit page.
![image](https://github.com/user-attachments/assets/617efddb-5abb-48b5-9510-f4f83980855c)

Select Boolean an drag to the page.
![image](https://github.com/user-attachments/assets/59092922-0e54-4609-b6b0-ebedb1a1e028)

Click on visit page on the **user prompt**
![image](https://github.com/user-attachments/assets/9b4759a3-3ce3-4b4b-b043-ef33d363dcba)

If we click on **No** and submit.

Now the user selects **no** *the computer was not isolated, please investigate* message was sent over to **Slack**
We need to build our variable which in our case is computer name.
Lets build that.
Click **Trigger** and drag it to the storyboard.

![image](https://github.com/user-attachments/assets/45dddb7f-d57c-4a10-8c52-fb6e83bb331d)

Change the name to **No** and connect it to the page.

Select **Rules** and click on **+** buttom
Select User prompt > body > body > isolate

![image](https://github.com/user-attachments/assets/a5bc2052-1cb5-435b-9f13-050bd53e17a0)

The **result** on lowe left corner shows **false**
If it does not show **false** test again the page you will view the option.
Click outside of the box to close it.

![image](https://github.com/user-attachments/assets/960e24c4-3ccb-4d01-bc6c-ada4ff96e393)

Copy the **Slack message** from the storyboard and paste it on the storyboard to make a copy of it and edit the message.
![image](https://github.com/user-attachments/assets/1c88a071-a2dc-48c0-b059-63822c718405)

Connect the **Trigger** to the **Slack message.**

Goto **user prompt** and test it
Select **no** and press submit.

![image](https://github.com/user-attachments/assets/576dbb34-74f4-496c-88b1-19f0a9e74b17)


We goto **Slack** and see the message.
The message is showen it **Slack** it means our connection is working properly.

![image](https://github.com/user-attachments/assets/6808d57b-1c9a-4f02-b1a3-9cd9fbcd985c)

Create another **Trigger**
Re-run the test
This time select **Yes** and submit.

Click on event.
Expand user prompt.
Expand body.
This time we have selected **Yes**, so the *do_yo_want_to_isolate:* is showing **true**
![image](https://github.com/user-attachments/assets/2e1a477a-1041-43ce-a3ed-b4eab08b7017)

Connect the **Trigger** to the **User Prompt**
![image](https://github.com/user-attachments/assets/2cced159-ad60-475e-ad32-a061b61cfd29)


Goto template and select **LimaCharlie** and drag it to storyboard.

Now the question is How will **LimaCharlie** will know which machine to isolate.

Search **Isolate Sensor**

Add the path of the **sid** in the URL section.

![image](https://github.com/user-attachments/assets/af7620a4-eaa7-44c4-b795-507c015b0f9d)

The result shows **null**, so we need to re-run the playbook while being connected to the new application.



Goto ***webhook** events and re-emit.

Goto **User Prompt** and select **yes** and submit.
We can see the error on **Isolate Sensor** we did not do any configuration other than changing the url.

![image](https://github.com/user-attachments/assets/d344bc72-719d-43b3-b42f-bd1fb5142054)

Now if we click on the link we can see our sensor id  as a result at the bottom.

![image](https://github.com/user-attachments/assets/6b8252d8-fa7a-4766-9ee8-3cd9f785912e)

Authorization is looking for credentials that means we need to authenticate **LimaCharlie**

![image](https://github.com/user-attachments/assets/785a030c-e213-451a-bb32-f6aae82cd2f9)

**For Credentials Authorization**
Open **Tines** in new tab.
Click on credentials.
Click on **New.**
Search for **LimaCharlie.**
![image](https://github.com/user-attachments/assets/61e80cf9-76c0-4399-bf42-86aa86053527)

Since **LimaCharlie** is not present here.
We need to goto the **LimaCharlie**
Click on **Access Management** and select **Rest API**
Copy **Org JWT**
![image](https://github.com/user-attachments/assets/f4e75135-e605-4e7e-ba5f-475253a44ce8)


**On Tines**
Click on **New** and select **text**
![image](https://github.com/user-attachments/assets/98dc560c-d2b2-4d69-956e-2dfc6f56556b)

Paste the JWT in value.
For URL: *.limacharlie.io
And Save it.

Now we have our credentials.
![image](https://github.com/user-attachments/assets/8112b81a-d774-473c-b196-a436a0c2573b)


**Back to our storyboard tab and refresh**
On credentials press connect for **LimaCharlie**
![image](https://github.com/user-attachments/assets/07a8d987-6706-4a5b-92dd-32ebaec12752)

Now **LimaCharlie** Credentials are added.

![image](https://github.com/user-attachments/assets/0bc9feae-e8fb-4605-b059-a42fecb23213)


**On LimaCharlie**
Select **Sensor**
In Network Access section it is shown **Isolate From Network** for **Allowed**


 **On Tines**
 So lets go to our play book and re run it.
 Select **Yes** in isolate the pc and submit.

![image](https://github.com/user-attachments/assets/3b0a02d2-5aff-4d45-8f2c-c9c909343bce)


**On LimaCharlie**
Select **Sensor**
In Network Access section it is shown **Isolated** and it shows the option to **Rejoin Network**
![image](https://github.com/user-attachments/assets/0acd3e7e-3530-4b7d-97a2-53016ca57c12)


**On Infected system**
We need to check if the infected system is actually disconnected from the network or not.
Open powershell and try to ping, we will not be able to ping.
It shows **General failure**
![image](https://github.com/user-attachments/assets/2c9d684a-8bb8-4dc3-9ced-9b41244ac1ab)














































  
