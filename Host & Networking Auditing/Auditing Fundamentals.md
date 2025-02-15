# Introduction to Security Auditing

## Overview of Security Auditing

### What is Security Auditing?

- Security Auditing is a systematic process of evaluating and verifying the security measures and controls in place within an organization to ensure they are effective, appropriate, and compliant with relevant standards, policies and regulaions.
- It involves reviewing various aspects of the organization's information systems, networks, application and operational procedures to identify vulnerabilities, weaknesses and areas for improvement.

### Importance of Security Auditing

1. **Identifying Vulnerabilities and Weaknesses:**
- Security audits help uncover vulnerabilities and weaknesses in an organizaion's information systems and infrastructure that could be exploited by attackers.
- Regular audits ensure that security controls are effective and up-to-date, minimizing the risk of breaches.

2. **Ensuring Compliance:**
- Organizations must comply with various regulatory requirements an industry standards to protect sensitive data and maintain trust with customers and stakeholders.
- Security audits help verify compliance with standards such as GDPR. HIPAA, PCI DSS, and ISO 27001, avoiding legal and finanical penalties.

3. **Enhancing Risk Management:**
- Audits provide a comprehensive assessment of an organization's security posture, identifying and prioritizing risks based on heir potential impact.
- Effective risk management strategies can be developed and implemented based on audit findings to mitigate identified risks.

4. **Improving Security Policies & Procedures:**
- Security audits review the effectiveness of existing security policies and procedures, identifying areas for improvement.
- Updated and robust security policies and procedures help create a strong security culture within the organization.

5. **Supporting Business Objectives:**
- A strong security posture supports overall business objectives by ensuring that critical business operations are protected from disruptions caused by security incidents.
- Audits help build customer trust and confidence, as clients are assured that their data is handled securely and responsibly.

6. **Continous Improvement:**
- Security auditing is not a one-time activity but an ongoing process that promotes continous improvement.
- Regular audits ensure that security measures evolve o address new threas and vulnerabilities, maintaining a proactive approach to security.

## Essential Terminology

![grafik](https://github.com/user-attachments/assets/7c738c49-2ddf-4265-9031-2eefec91656e)

![grafik](https://github.com/user-attachments/assets/a349322b-7078-47c9-8d2d-1a51aa5b4eba)

## Security Auditing Process/Lifecycle

1. **Planning and Preparation**
- Define Objectives and Scope: Determine the goals of the audit and the specific systems, processes, and controls to be evaluated.
- Gather Relevant Documentation: Collect policies, procedures, network diagrams, and previous audit reports.
- Establish Audit Team and Schedule: Assemble the audit team and set a timeline for the audit activities.

2. **Information Gathering**
- Review Policies and Procedures: Examine the organization's security policies, procedures, and standards.
- Conduct Interview key personnel to understand security practices and identify potential gaps.
- Collect Technical Information: Gather data on system configurations, network architecture, and security controls.

3. **Risk Assessment**
- Identify Assets and and Threats: List critical assets and potential threats to those assets.
- Evaluate Vulnerabilities: Assess existing vulnerabilities in systems and processes.
- Determine Risk Levels: Assign risk levels based on the likelihood and impact of identified threats and vulnerabilities.

4. **Audit Execution**
- Perform Technical Testing: Conduct technical assessments such as vulnerability scans, pentests, and confiugration reviews.
- Verify Compliance: Check adherence to relevant regulations and standards.
- Evaluate Controls: Assess the effectiveness of security controls and practices.

5. **Analysis and Evaluation**
- Analyze Fidings: Review data collected during the audit to identify security weaknesses and areas for improvement.
- Compare against Standards: Measure the organization's security posture against industry standards and best practices.
- Prioritize Issues: Rank findings based on their severity and potential impact on the organization.

6. **Reporting**
- Document Findings: Create a detailed report outlining audit findings, including identified vulnerabilities, non-compliance issues, and ineffective controls.
- Provide Recommendations: Offer actionable recommendations to address identified issues and enhance security.
- Present Results: Share the audit report with relevant stakeholders and discuss key findings and recommendations.

7. **Remediation**
- Develop Remediation Plans: Work with the organization to create plans for addressing the audit findings.
- Implement Changes: Assist in implementing recommended changes and improvements.
- Conduct Follow-Up Audits: Schedule follow audits to ensure that remediation efforts have been completed and are effective.
- Monitor and Update: Continously monitor the organization's security posture and update security measures as needed.

### Security Auditing Lifecycle

![grafik](https://github.com/user-attachments/assets/860cd649-6af5-44ca-8da3-a1935a56c51c)

## Types of Security Audits

![grafik](https://github.com/user-attachments/assets/8c4ebc56-d391-4edd-9c14-04eca8116c19)

![grafik](https://github.com/user-attachments/assets/424dfbe2-79ce-4a80-8fe5-42bd2e6f43a8)

## Security Auditing & Penetration Testing

![grafik](https://github.com/user-attachments/assets/c35078f9-b9d4-4dcf-a9ea-3a9a9377382c)

### Sequental Approach

**Perform Security Audit First:** Companies often coduct a security audit first to elevate their overall security posture, ensure compliance with regulations, and identify areas for improvement in policies and procedures.

**Conduct Penetration Test Afterwards:** Based on the findings of the audit, a penetration test may be performed to assess the effectiveness of technical controls and identify specific vulnerabilities.

**Advantages**
- Provides a comprehensive view of security from both policy and technical perspectives.
- Identifies and addresses gaps in both procedural and technical controls.
- Helps prioritize remediation efforts based on audit findings.

### Combined Appraoch

**Integrate Security Audit and Penetration Testing:** Some organizations choose to combine security audits and penetration tests, often through a holistic security assessment that incorporates both elements.

**Advantages**
- Streamlines the assessment process by combining policy, procedural, and technical evaluations.
- Provides a more complete picture of the organization's security posture in a single engagement.
- Can be more efficient and cost-effective by addressing both compliance and technical vulnerabilities simultaneously.

### Example: Sequential Approach

- Consider a fictional organization, "SecurePayments Inc.", which processes credit card transactions and must adhere to PCI DSS standards.
- In this example, "SecurePayments Inc." is using a sequential approach to assess their overall security posture. The organization has already performed a security audit through an independent audit firm and are using the findings in the audit report as the basis of their remediation plan/efforts.
- As part of their remediation plan, the organization has decided to hire you (or your firm) to perform a penetration test with a focus on ensuring PCI DSS compliance.
- The extenral audit performed by the independent audit firm outloined the following findings:
  - Inadequate encryption for cardholder data in transit.
  - Weak/inadequate network security controls and traffic monitoring.
  - Weak access control policies that allows excessive permissions,
  - Outdated incident response procedures.
- The corresponding recommendations for the findings outlined are:
  - Implement strong encryption protocols for data in transit.
  - Revise access control policies to follow the principle of least privilege.
  - Update and test incident response procedures regularly.
 
The company followed the Security Audit lifecycle/process outlined in the "Security Auditing Process/Lifecycle video and made the necessary improvements based on the recommendations.

**SecurePayments Inc. - Penetration Test**

**Objectives:**
- After making the necessary changes/improvements based on the findings and recommendations in the external audit report, "SecurePayments Inc.," has hired you to test the technical controls and security measures implemented based on audit findings to verify whether they are effective.

**Phase 1: Planning and Preparation:**
During the initial phase, you identify that the PCI DSS scope includes the cardholder data environment (CDE). You review SecurePayments Inc.'s network diagrams and PCI DSS self-assessment questionaires to understand their current security measures and compliance status.
**Objectives:**
- Define the scope of the pentest to focus on the areas identified in the audit, such as network security and application vulnerabilities.
- Set up a testing schedule and inform stakeholders.

**Phase 2: Information Gathering and Reconnaissance:**
- You gather information on SecurePayments Inc.'s security policies, such as their access control policies, encryption standards, and incident response procedures.
- You also review their most recent PCI DSS audit report to identify areas of concern highlighted by auditors.

**Phase 3: Penetration Testing Execution:**
- Conduct network scanning, enumeration and vulnerability assessments to identify weaknesses, misconfigurations or vulnerabilities.
- Attempt exploitation of identified vulnerabilities to asses their impact.
- Test the effectiveness of newly implemented encryption and access controls.

**Phase 4: Findings and Recommendations:**
- Outcome: The pentest uncovers additional vulnerabilities:
  - An exposed administrative interface that allows unauthorized access.
  - SQL injection vulnerabilities in a customer-facing web application.
 
- Recommendations:
  - Secure the administrative interface by implementing additional authentication and access controls.
  - Patch the SQL injection vulnerabilities and conduct a thorough review of application security.
 
**Summary of Sequential Approach**
- Security Audit Results:
  - Identified compliance gaps and policy deficiencies.
  - Provided recommendations for improved security policies and procedures.
- Penetration Testing Results:
  - Revealed specific technical vulnerabilities.
  - Offered targeted recommendations to address these technical weaknesses.


# Governance, Risk & Compliance

## Governance, Risk & Compliance (GRC)

- Governance, Risk & Compliance (GRC) is a comprehensive framework used by organization to manage and align their governance practices, risk management strategies, and compliance with regulatory requirements.
- The holistic approach helps organizations maintain transparency, accountability, and resilience in an increasingly complex regulatory environment.

**Governance**
- Governance refers to the framework of policies, procedures, and practices that ensure an organization achieves its objectives, managages its risks, and complies with legal and regulatory requirements.
- Components:
  - Policy Development: Creating clear, comprehensive security policies.
  - Roles and Responsibilities: Defining roles and responsibilities for security management.
  - Accountabilitiy: Establishing accountability mechanisms for security performance.

 **Risk**
- Risk management involves identifying, assessing, and mitigating risks that could negatively impact an organization's assets and operations.
- Components:
  - Risk Identification: Recognizing potential threats and vulnerabilities.
  - Risk Assessment: Evaluating the likelihood and impact of identified risks.
  - Risk Migration: Implementing measures to reduce or eliminate risks.

**Compliance**
- Compliance ensures that an organization adheres to relevant laws, regulations, and industry standards.
- Components:
  - Regulatory Requirements: Meeting legal obligations such as GDPR, HIPAA, or PCI DSS.
  - Internal Policies: Adhering to internal security policies and procedures.
  - Audits and Assessments: Conducting regular reviews to ensure compliance.
 
### Importance of GRC in Penetration Testing
- Comprehensive Security Assessment: Understanding GRC helps testers conduct more thorough and relevant assessments.
- Enhanced Reporting: Knowledge of GRC allows testers to frame their findings in the context of organizational policies, risk management, and compliance requirements.
- Strategic Recommendations: Testers can provide more strategic recommendations that align with the organization's GRC framework, helping to strengthen overall security posture.

## Common Standards, Frameworks & Guidelines

- Frameworks: Provide a structured approach to implementing security practices, often flexible and adaptable to various organizations and industries.
- Standards: Set specific requirements and criteria that must be met to achieve compliance; often mandatory in regulated industries.
- Guidelines: offer recommended practices and advice to improve security; generally not mandatory but considered best practices.

### Frameworks

**NIST Cybersecurity Framework (CSF)**
- Overview: A set of guidelines and best practices developed by the National Institute of Standards and Technology (NIST) to help organizations manage and reduce cybersecurity risk.
- Key Focus: Core functions include Identify, Protect, Detect, Respond and Recover.

**COBIT (Control Objectives for Information and Related Technologies)**
- Overview: A framework for developing, implementing, monitoring and improving IT governance and management practices.
- Key Focus: Aligning IT goals with business objectives, managing IT risks, and ensuring compliance with regulations.

### Standards

**ISO/IEC 27001**
- Overview: An international standard for information security management systems (ISMS) that outlines best practices for managing and protecting sensitive information.
- Key Focus: Establishing, implementing, maintaining and continually improving an ISMS.

**PCI Data Security Stanard (PCI DSS)**
- Overview: A set of security standards designed to protect payment card information and ensure secure processing of credit card transactions.
- Key Focus: Requirements for protecting cardholder data, maintaining a secure network, and implementing robust access control measures.
- Legal Requirement: Required for organizations that handle credit card transactions.

**GDPR (General Data Protection Regulation)**
- Overview: A regulation in the European Union that governs data protection and privacy for individuals within the EU and the European Economic Area (EAA).
- Key Focus: Data protection principles, right of data subjects, and obligations for data controllers and processors.
- Legal Requirement: Required for organizations processing personal data of individuals within the EU/EEA.

### Guidelines

**CIS Controls (Center for Internet Security Controls**
- Overview: A set of best practices and actionable steps to help organizations improve their cybersecurity posture.
- Key Focus: Foundational and advanced security controls organized into categories such as basic, foundational, and organizational controls.

# From Auditing to Penetration Testing

## Phase 1 - Developing a Security Policy

**Background:**
- Company: SecureTech Solutions

**Description:**
- SecureTech Solutions is a fictitious cybersecurity consultancy that specializes in securing IT infrastructure for various clients.
- In this example, we will be demonstrating the process of developing a security policy for Linux servers, performing a risk assessment using the NIST SP 800-53 framework, perfoming a security audit and testing the remediations.
- The example will guide you thorugh the entire process, from initial policy creation to auditing and penetration testing, highlighting the importance of compliance with industry standards.

**Objectives:**
- Establish a baseline security policy for Linux servers that aligns with NIST SP 800-53 guidelines, ensuring that servers are configured and managed securely.
- This policy should ensure that Linux servers are secure and protected from unauthorized access, vulnerabilities, and other security threats.
- It will be used to establish baseline security requirements for configuring, maintaining, and monitoring Linux servers within the organization, aligned with NIST SP 800-53.

**Security Policy Development Process: Requirements Gathering**
- Purpose: Define the purpose and scope of the security policy.
- Access Control: Outline user account management, authentication methods, and privilege management.
- Audit and Accountability: Specify logging requirements and log review procedures. Configuration Management: Define baseline configurations, software update practices, and change management.
- Identification and Authentication: Enforce strong passwords, policies and unique user identification.

**Simple Security Policy for Linux Servers Aligned with NIST SP 800-53**

![grafik](https://github.com/user-attachments/assets/c27df8de-c401-489c-bcf8-e059a2d8a046)

![grafik](https://github.com/user-attachments/assets/903431a6-f05b-4679-8557-1751b08f11dd)

![grafik](https://github.com/user-attachments/assets/febb5eff-66ca-492f-8afc-29b75ef82c6a)
