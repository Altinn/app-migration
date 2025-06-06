---
name: 'Sub-issue: Valider sikkerhetskrav'
about: Sub-issue mal for validering av sikkerhetskrav.
title: Valider sikkerhetskrav
labels: ''
assignees: ''
type: 'Task'
---

### Architecture, Design and Threat Modeling

- [ ] V1.1.3: Verify that all user stories and features contain functional security constraints, such as "As a user, I should be able to view and edit my profile. I should not be able to view or edit anyone else's profile"
- [ ] V1.1.4: Verify that major data flows as well as usage of other components (Altinn products and third party products/services) are documented and justified.
- [ ] V1.1.5: Verify definition and security analysis of the application's high-level architecture and all connected remote services.
- [ ] V1.2.2: Verify that communications between application components, including APIs, middleware and data layers, are authenticated. Components should have the least necessary privileges needed.
- [ ] V1.5.3: Verify that input validation is enforced on a trusted service layer.
- [ ] V1.6.2: Verify that Azure Key Vault is used to protect key material and other secrets.
- [ ] V1.11.1: Verify that application components are documented and that the documentation describes the business or security functions they provide.
- [ ] V1.11.2: Verify that state is not shared across sessions. Consider integrity checks for all high-value transactions to avoid potential race conditions.

### Authentication

- [ ] V2.10.4: Verify that passwords, integrations with databases and third-party systems, seeds and internal secrets, and API keys are stored in Azure Key Vault and not included in the source code or stored within source code repositories.

### Access Control

- [ ] V4.1.3: Verify that the principle of least privilege exists - users should only be able to access functions, data files, URLs, controllers, services, and other resources, for which they possess specific authorization. This implies protection against spoofing and elevation of privilege.
- [ ] V4.3.3: Verify the application has additional authorization (such as step up or adaptive authentication) for lower value systems, and / or segregation of duties for high value applications to enforce anti-fraud controls as per the risk of application and past fraud.

### Validation, Sanitization and Encoding

- [ ] V5.1.3: Verify that all input (HTML form fields, REST requests, URL parameters, HTTP headers, cookies, batch files, RSS feeds, etc) is validated using positive validation (allow lists).
- [ ] V5.1.4: Verify that structured data is strongly typed and validated against a defined schema including allowed characters, length and pattern (e.g. credit card numbers, e-mail addresses, telephone numbers, or validating that two related fields are reasonable, such as checking that suburb and zip/postcode match).
- [ ] V5.2.2: Verify that unstructured data is sanitized to enforce safety measures such as allowed characters and length.
- [ ] V5.2.3: Verify that the application sanitizes user input before passing to mail systems to protect against SMTP or IMAP injection.
- [ ] V5.2.4: Verify that the application avoids the use of eval() or other dynamic code execution features. Where there is no alternative, any user input being included must be sanitized or sandboxed before being executed.
- [ ] V5.2.6: Verify that the application protects against SSRF attacks, by validating or sanitizing untrusted data or HTTP file metadata, such as filenames and URL input fields, and uses allow lists of protocols, domains, paths and ports.
- [ ] V5.3.6: Verify that the application protects against JSON injection attacks, JSON eval attacks, and JavaScript expression evaluation.
- [ ] V5.3.8: Verify that the application protects against OS command injection and that operating system calls use parameterized OS queries or use contextual command line output encoding.
- [ ] V5.3.10: Verify that the application protects against XPath injection or XML injection attacks.
- [ ] V5.5.3: Verify that deserialization of untrusted data is avoided or is protected in both custom code and third-party libraries (such as JSON, XML and YAML parsers).

### Stored Cryptography

- [ ] V6.4.1: Verify that Azure Key Vault is used to securely create, store, control access to and destroy secrets.
- [ ] V6.4.2: Verify that key material is not exposed to the application but instead uses an isolated security module like a vault for cryptographic operations.

### Error Handling and Logging

- [ ] V7.1.1: Verify that the application does not log credentials or payment details. Session tokens should only be stored in logs in an irreversible, hashed form.
- [ ] V7.1.2: Verify that the application does not log other sensitive data as defined in Personopplysningsloven and Digdir's policies. In general, logging of personal identifiable information (PII) to technical logs should be avoided if possible.
- [ ] V7.1.4: Verify that each log event includes necessary information that would allow for a detailed investigation of the timeline when an event happens.
- [ ] V7.3.1: Verify that all logging components appropriately encode data to prevent log injection.
- [ ] V7.4.2: Verify that exception handling (or a functional equivalent) is used across the codebase to account for expected and unexpected error conditions.

### Data Protection

- [ ] V8.1.3: Verify the application minimizes the number of parameters in a request, such as hidden fields, Ajax variables, cookies and header values.

### Communication

- [ ] V9.2.3: Verify that all connections to external systems are authenticated - e.g. by verfifying the external system's TLS certificate (including signature chain and revocation status).

### Malicious Code

- [ ] V10.2.1: Verify that the application source code and third party libraries do not contain unauthorized phone home or data collection capabilities.
- [ ] V10.3.2: Verify that the application employs integrity protections, such as code signing or subresource integrity. The application must not load or execute code from untrusted sources, such as loading includes, modules, plugins, code, or libraries from untrusted sources or the Internet.

### Business Logic

- [ ] V11.1.1: Verify that the application will only process business logic flows for the same user in sequential step order and without skipping steps.
- [ ] V11.1.5: Verify the application has business logic limits or validation to protect against likely business risks or threats, identified in the epic's risk assessment or threat modeling activities. Verify that all Github issues representing mitigating actions are closed.

### Files and Resources

- [ ] V12.1.1: Verify that the application will not accept large files that could fill up storage or cause a denial of service.
- [ ] V12.1.2: Verify that the application checks compressed files (e.g. zip, gz, docx, odt) against maximum allowed uncompressed size and against maximum number of files before uncompressing the file.
- [ ] V12.2.1: Verify that files obtained from untrusted sources are validated to be of expected type based on the file's content.
- [ ] V12.3.1: Verify that user-submitted filename metadata is not used directly by system or framework filesystems and that a URL API is used to protect against path traversal.
- [ ] V12.3.2: Verify that user-submitted filename metadata is validated or ignored to prevent the disclosure, creation, updating or removal of local files (LFI).
- [ ] V12.3.3: Verify that user-submitted filename metadata is validated or ignored to prevent the disclosure or execution of remote files via Remote File Inclusion (RFI) or Server-side Request Forgery (SSRF) attacks.
- [ ] V12.3.4: Verify that the application protects against Reflective File Download (RFD) by validating or ignoring user-submitted filenames in a JSON, JSONP, or URL parameter, the response Content-Type header should be set to text/plain, and the Content-Disposition header should have a fixed filename.
- [ ] V12.3.5: Verify that untrusted file metadata is not used directly with system API or libraries, to protect against OS command injection.
- [ ] V12.3.6: Verify that the application does not include and execute functionality from untrusted sources, such as unverified content distribution networks, JavaScript libraries, node npm libraries, or server-side DLLs.
- [ ] V12.4.2: Verify that files obtained from untrusted sources are scanned by antivirus scanners to prevent upload and serving of known malicious content.

### Configuration

- [ ] V14.2.4: Verify that third party components come from pre-defined, trusted and continually maintained repositories.
