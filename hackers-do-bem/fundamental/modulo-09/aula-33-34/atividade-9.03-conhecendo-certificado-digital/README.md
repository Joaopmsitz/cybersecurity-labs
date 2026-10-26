# Activity 9.02 — Issuing Digital Certificates Using a Certificate Authority

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 09  
> **Classes:** 33–34  
> **Environment:** Windows Server 2022  
> **Status:** Completed

## Objective

Use the Certificate Authority created in the previous activity to configure a certificate template, make it available on the CA, and configure auto-enrollment through a Group Policy Object (GPO).

At the end of the activity, `gpupdate /force` was used to apply the configured policies and check certificate issuance in the environment.

## Environment

- **Operating system:** Windows Server 2022
- **Service:** Active Directory Certificate Services (AD CS)
- **Certificate Authority:** `aluno-DC01-CA`
- **Domain:** `aluno.hacker.com`
- **Created template:** `ALUNO COMPUTADOR`
- **GPO:** `COMPUTADOR: Politica de Inscricao de Certificado`
- **Mechanism:** Certificate Auto-Enrollment

## 1. Accessing the Certificate Authority Templates

In the **Certification Authority (Local)** window, the following authority was expanded:

```text
aluno-DC01-CA
```

The following option was then accessed:

```text
Certificate Templates → Manage
```

The **Certificate Template Console** window opened.

## 2. Duplicating the Template

In the list of available templates, the following template was located:

```text
Workstation Authentication
```

The template was right-clicked, and the following option was selected:

```text
Duplicate Template
```

Duplicating the template made it possible to create a new template based on the settings of the existing one.

## 3. Creating the ALUNO COMPUTADOR Template

In the **Properties of New Template** window, the following tab was opened:

```text
General
```

The **Template display name** field was changed to:

```text
ALUNO COMPUTADOR
```

This name identifies the new template within the certificate infrastructure.

## 4. Configuring the Subject Name

The following tab was opened:

```text
Subject Name
```

The following option was enabled:

```text
User principal name (UPN)
```

This setting allows the UPN to be used in the identity information associated with the issued certificate.

## 5. Configuring Permissions

The following group was selected in the **Security** tab:

```text
Domain Computers (ALUNO\Domain Computers)
```

The following **Allow** permissions were enabled for this group:

```text
Read
Autoenroll
```

The changes were applied by selecting **Apply** and **OK**.

After configuration, the new template appeared as:

```text
ALUNO COMPUTADOR
```

## 6. Making the Template Available on the CA

Back in the **Certification Authority (Local)** window, the following option was accessed:

```text
Certificate Templates → New → Certificate Template to Issue
```

In the **Enable Certificate Templates** window, the following template was selected:

```text
ALUNO COMPUTADOR
```

The operation was confirmed by selecting **OK**.

The template then became available for certificate issuance by the Certificate Authority.

## 7. Verifying the Template

After selecting the following folder:

```text
Certificate Templates
```

the `ALUNO COMPUTADOR` template was visible in the right-hand pane.

This indicates that the CA is configured to use this template when issuing certificates.

## 8. Opening Group Policy Management

In Server Manager, the following option was accessed:

```text
Tools → Group Policy Management
```

The following domain tree was expanded:

```text
Forest: aluno.hacker.com
└── Domains
    └── aluno.hacker.com
        └── Group Policy Objects
```

A new Group Policy Object was created.

## 9. Creating the GPO

The new GPO was named:

```text
COMPUTADOR: Politica de Inscricao de Certificado
```

The policy was created under:

```text
Group Policy Objects
```

## 10. Editing the Policy

The newly created GPO was opened by selecting **Edit**.

In the **Group Policy Management Editor**, the following path was followed:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Public Key Policies
```

The following setting was selected:

```text
Certificate Services Client – Auto-Enrollment
```

## 11. Configuring Auto-Enrollment

In the **Certificate Services Client – Auto-Enrollment** settings, the following field was changed:

```text
Configuration Model
```

Its value was changed from:

```text
Not configured
```

to:

```text
Enabled
```

The options related to certificate renewal and updating were also enabled:

```text
Renew expired certificates...
Update certificates...
```

The changes were confirmed by selecting **Apply** and **OK**.

## 12. Configuring the Automatic Certificate Request

In the right-hand pane of the **Group Policy Management Editor**, the following option was accessed:

```text
Automatic Certificate Request Settings
```

It was right-clicked, and the following options were selected:

```text
New → Automatic Certificate Request...
```

The wizard was advanced by selecting **Next** until it was completed with **Finish**.

## 13. Updating the Policies

To apply the configured settings immediately, the Command Prompt was opened.

The following command was executed:

```cmd
gpupdate /force
```

This command forces an update of the Group Policies applicable to the computer and user.

## 14. Verifying the Policy Update

After the command was executed, Windows displayed:

```text
C:\Users\Administrator>gpupdate /force
Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

This result indicates that both computer policy and user policy were updated successfully.

## 15. Verifying Certificate Issuance

After the policy update, the following window was reopened:

```text
certsrv - [Certification Authority (Local)]
```

The following folder was inspected:

```text
Issued Certificates
```

A certificate was found in the list.

This demonstrates that the configured enrollment policy had been applied and that the Certificate Authority was being used to issue a certificate.

## 16. Ending the Server Session

After verifying certificate issuance, the RDP session with the Windows Server 2022 machine used as the server was closed.

The environment was left ready for the next activity, in which the issued certificate would be examined on the Windows Server 2022 client.

## Evidence — Step 17

The evidence requested for this activity corresponds to step 17 and shows the execution of `gpupdate /force` and the successful policy update.

Required caption before the screenshot:

> Screenshot for Activity 9.2: execution of `gpupdate /force`, demonstrating that computer and user policies were updated successfully.

```text
C:\Users\Administrator>gpupdate /force
Updating policy...

Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

Evidence for this activity is included in the PDF for Module 9, Classes 33–34.

[View Evidence — Classes 33–34](../evidencias.pdf)

## Concepts Applied

### Certificate Template

A Certificate Template defines the characteristics and rules used by a Certificate Authority to issue specific types of certificates.

In this lab, the following template was created:

```text
ALUNO COMPUTADOR
```

It was based on the existing `Workstation Authentication` template.

### Auto-Enrollment

Auto-enrollment allows certificates to be requested and managed automatically by computers or users that meet the conditions defined in domain policies.

### Group Policy

Group Policies (GPOs) allow settings to be centrally distributed to computers and users belonging to a domain.

In this exercise, a GPO was used to configure certificate auto-enrollment behavior.

### Certificate Authority

The `aluno-DC01-CA` CA, configured in the previous activity, was used to make the template available and issue certificates to domain computers.

## Activity Workflow

```text
Workstation Authentication Template
              │
              ▼
        Duplicate Template
              │
              ▼
       ALUNO COMPUTADOR
              │
              ▼
        Publish on the CA
              │
              ▼
          Create GPO
              │
              ▼
         Auto-Enrollment
              │
              ▼
         gpupdate /force
              │
              ▼
      Certificate Issuance
```

## Result

The following template was created and made available on the Certificate Authority:

```text
ALUNO COMPUTADOR
```

A Group Policy Object was also configured to enable certificate auto-enrollment for `Domain Computers`.

The policy application was confirmed by the following messages:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

The CA's **Issued Certificates** folder was subsequently used to verify certificate issuance.

---

[Back to Classes 33–34](../) · [Back to Module 9](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
