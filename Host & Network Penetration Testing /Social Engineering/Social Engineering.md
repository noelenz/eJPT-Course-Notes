# Social Engineering

## Introduction to Social Engineering

### What is Social Engineering?

- In the context of pentesting and red teaming, social engineering is a technique used to manipulate individuals or employees within an organization to gain unathorized access to sensitive information.
- It exploits human psychology, trust, and vulnerabilities to deceive targets into performing actions that compromise security, either through information disclosure or by performing specific actions that mayy seem innocuous at first glance.
- Social engineering attacks aim to bypass technical controls by targeting the weakest link in the security chain: the human element.
- The premise of social engineering is to exploit the human element, in other words, putting people or employees in situations where they will rely on their base insticts and most common forms of social interaction like:
  - The desire to be helpful
  - The tendency to trust people
  - The desire for approval
  - The fear of getting in trouble
  - Avoiding conflict or arguments
- By preying on the human element of system access, most times, attackers do not have to navigate around the security perimeter of an organization.
- Attackers/Pentesters just need to engage with employees inside the company to do their bidding for them.
- Instead of spending countless hours trying to infiltrate system/networks through traditional server-side attacks like brute-force attacks, attackers can leverage social engineering to yield information or facilitate the execution of malware inside the company network in a matter of minutes.

### Social Engineering & Social Media

- The advent and adoption of Social Networking as a form of communication has vastly improved the ability and effectiveness of attackers (likewise pentesters) to perform social engineering attacks as employees/targets can be easily contracted by anyone in the world with ease.
- Furthermore, Social Networks have also led to the rise of employees advertently/inadvertently exposing a lot of private information that can be used by attackers in aid of their social engineering attacks (Emails, phone numbers, addresses etc.).

### Social Engineering & Pentesting

- While social engineering has been a very viable attack vector for attackers, it has often been overlooked by pentesters until recently.
- Contextualizing and operationalizing social engineering as a valid attack vector in pentesting is a vital skill set to possess as a modern pentester.
- In pentesting and red teaming exercises, phishing simulations are valuable for assessing an organization's susceptibility to social engineering attacks and identifying areas for improvement in security awareness and controls


### Types of Social Engineering


![image](https://github.com/user-attachments/assets/90239002-2a3f-401b-be79-f2a620103b57)


### Phishing

- Phishing is one of the most prevalent and effective social engineering attacks used in pentesting and red teaming. It typically involves the following steps:
  1. **Planning & Reconnaissance:** Attackers research the target organization to identify potential targets, gather information about employees, and understand the organization's communication channels and protocols.
  2. **Message Crafting:** Attackers create deceptive emails or messages designed to mimic legitimate communications from trusted sources, such as colleagues, IT departments, or financial institutions. These messages often include urgent or compelling language to evoke a sense of urgency or fear.
  3. **Delivery:** Attackers send phishing emails or messages to targeted individuals wihtin the organization, using techniques to bypass spam filters and security controls. They may also leverage social engineering tactics to increase the likelihood of recipients opening the messages.
  4. **Deception & Manipulation:** The phishing messages contain malicious links, attachements, or requests for sensitive information. Recipients are decieved into clicking on links, downloading attachements, or providing login credentials under fals pretenses.
  5. **Exploitation:** Once the victim interacts with the phishing message, attackers exploit vulnerabilities in the target's systems or applications to gain unauthorized access, install malware, or steal sensitive information.

### Spear-Phishing

- Spear phishing is a targeted form of phishing attack that tailors malicious emails or messages to specific individuals or groups wihtin an organization.
- Unlike traditional phishing attacks, which cast a wide net and aim to deceive as many recipients as possible, spear phishing attacks are highly personalized and customized to exploit the unique characteristics, interests, and relationships of the intended targets.

### Spear-Phishing Process

1. **Target Selection & Research:**
   - Attackers carefully select their targets based on specific criteria, such as job roles, departments, or organizational hierarchies.
   - Extensive reconnaissance is conducted to gather information about the targets, including names, job titles, roles, responsibilities, work relationships, and personal interests.
   - Publicly available sources, social media profiles, corportate directories, and leaked data may be mined to compile detailed profiles of the targets.

2. **Message Tailoring:**
   - Using the gathered information, attackers craft highly personalized and convincing emails or messages designed to appear legitimate and trustworthy.
   - The content of the messages may reference recent events, projects, or activities relevant to the target's role or interests to enhance credibility.
   - Attackers may impersonate trusted individuals, such as colleagues, supervisors, or external partners, to increase the likelihood of the targets opening the messages and taking the desired actions.

3. **Delivery:**
   - Spear phishing messages are delivered to the targeted individuals via email, social media, instant messaging platforms, or other communication channels.
   - Attackers employ tactics to bypass email security filters and anti-phishing mechanisms, such as using compromised or spoofed email accounts, exploiting zero-day vulnerabilities, or leveraging trusted third-party services.
  
---

## Pretexting

### What is Pretexing?

- Pretexting is the process of creating a false pretext or scenario to gain the trust of targets and extract sensitive information. This may involve impersonating authority figures, colleagues, or service providers to manipulate victims into divulging confidental data.
- Simply put, it is putting someone or an employee in a familiar situation to get them to divulge information.
- Unlike other forms of social engineering that rely on deception or coercion, pretexting involves the creation of a false narrative or context to establish credibility and gain the trust of the target.

### Characteristics of Pretexting

- **Flse Pretense:** The attacker creates a fictional story or pretext to deceive the target into believing that the interaction is legitimate and trustworthy. This pretext often involves impersonating someone with authority, expertise, or a legitimate reason for requesting information or assistance.
- **Establishing Trust:** The attacker uses the pretext to establish rapport and build trust with the target. This may involve leveraging social enigneering techniques, such as mirroring the target's language, tone, and behavior, to create a sense of familiarity and connection.
- **Manipulating Emotions:** Pretexting often exploits human emotions, such as curiosity, fear, urgency, or sympathy, to manipulate the target's behavior. By appealing to these emotions, the attacker can influence the target's decision-making process and increase compliance with their requests.
- **Information Gathering:** Once trust is established, the attacker seeks to extract sensitive information or access privileges from the target. This may involve posing as a trusted entity (e.g., colleague, vendor, service provider) and requesting information under the pretext of a legitimate need or emergency.
- **Maintaining Consistency:** To maintain the illusion of legitimacy, the attacker ensures that the pretext remains consistent and plausible thorughout the interaction.
- This may require careful planning, research, and improvisation to adapt to the target's responses and maintain credibility.

### Pretexting Examples:

**Tech Support Scam:** An attacker poses as a technical support representative from a legitimate company and contact indiviudals, claiming that their computer is infected with malware. The attacker convinces the target to provide remote access to their computer or install malicious software under the pretext of fixing the issue.

**Job Interview Scam:** An attacker pretends to be a recruiter or hiring manager from a reputable company and contacts jobs seekers, offering them fake job opportunities or conducting fraudulent job interviews. The attacker may request sensitive personal information or payment under the pretext of processing the job application.

**Emergency Situation:** An attacker fabrictes an emergency situation, such as a security breach, data leak, or system outage, and contacts employees, requesting immediate assistance or information. The attacker exploits the target's sense of urgency and concern to extract sensitive information or gain access to systems under the pretext of resolving the emergency.

### Importance and Impact

- Pretexting can be highly effective in bypassing technical controls and exploiting human vulnerabilities within organizations. It relies on psychological manipulation and social engineering tactics to decieve targets and achieve malicious objectives.
- Pretexting attacks can lead to data breaches, financial losses, reputational damage, and regulatory penalties for organizations. Therefore, it is essential for organizations to raise awareness about pretexting techniques, implement robust security policies and procedures, and provide training to employees to recognize and mitigate social engineering attacks.

### Pretexting Templates/Samples

**Corporate IT Department Upgrade**

- Pretext: The attacker impersonates a member of the company's IT department and sends an email to employees, claiming that the company's email system is being upgraded. The email instructs recipients to click on a link to update their email settings to avoid service disruptions.
- Objective: To trick employees into clicking on the malicious link, which leads to a phishing website where they are promted to enter their email credentials, allowing the attacker to steal their login information.


![image](https://github.com/user-attachments/assets/7a0845c6-cede-4e4a-ad39-b6d99e7341e3)


### References & Resources

- A library of pretexts to use on offensive phishing engagements
https://github.com/L4bF0x/PhishingPretexts/tree/master

## Phishing With Gophish

### Gophish

- Gophish is a framework for security professionals to simulate phishing attacks against their own organizations.

### Gophish Features

**Camapign Creation:** GoPhish allows users to create customized phishing campaigns tailored to their specific objectives and targets. Users can create multiple campaigns with different templates, email content, and target lists.

**Email Template Editor:** The platform provides a built-in email tempate editor with a WYSIWYG (What you see is what you get) interface, making it easy to design professional-looking phishing emails that mimic legitimate communications.

**Target Management:** Users can manage their target lists and segment them based on various criteria, such as department, role, or location. This allwos for targeted phishing campaigns that closely mirror real-world attack scenarious.

**Landing Page Creation:** GoPhish enables users to create phishing landing pages that mimic legitimate login portals or websites. These landing pages can be customized to capture credentials, personal information, or other sensitive data from targets.

**Tracking and Reporting:** The platform provides comprehensive tracking and reporting capabilities, allowing users to monitor the progress of their phishing campaigns in real-time. Users can track email opens, link clicks, and submitted data, and generate detailed reports for analysis.

**Scheduling and Automation:** GoPhish supports campaign scheduling and automation, allowing users to schedule campaign launches at specific dates and times or set up recurring campaigns for ongoing testing and assessment.

### References & Resources

- Gophish Website: https://getgophish.com/
- Gophish GitHub Repo: https://github.com/gophish/gophish
- Gophish Installation Guide: https://docs.getgophish.com/user-guide/installation

## Demo: Phishing with GoPhish

- We open base.html with notepad and delete the additional fonts, because it makes the Gophish web slower. We not delete locally stored fonts.
- We do the same for the login page and dashboard (if existent)
- In config.json we could specify a SSL certificate.
- In a real pentest, we would need to specify our Gophish server in the config.json file.
- We set use_tls to false in the config.json file.
- We delete the external resources in C:\inetpub\wwwroot\index.html

We open the Gophish executable. Starts up the server.

### GoPhish Dashboard

1. Setup the Sending Profile, for sending emails (who email is from). In our case:
   1. **Name:** Red Team
   2. **From:** info <support@demo.ine.local>
   3. **Host:** localhost:25 (netstat -ano, port 25 (mailserver) listening)
   4. **Username:** red@demo.ine.local
   5. **Password:** penetrationtesting

   We test the email. victim@demo.ine.local (Vic, Tim, Intern).

2. We set up a landing page which mimics a login page.
   2.1 **Name:** INE Password Reset
   2.2 **URL:** http://localhost:8080
   2.3 We select Capturing Submitted Data and we could also Capture Passwords (Checkmarking the window for Capturing Data.)
   2.4 Redirect

3. Creating E-Mail Template
   3.1 **Name:** INE Password Reset
   3.2 **Import Email:** We import the raw email content. Here we can also insert our pretext
   3.4 We could also add files.

4. New Group
   4.1 **Name: INE Employees:** Bulk Import Users (CSV)

5. Campaign
   5.1 Specify all the parameters
   5.2 **URL:** localhost port 80: http://localhost
   5.3 Setting the Date/Time when the campaign should be sent out
   5.4



