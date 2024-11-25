### Summary of the Report: Pentesting of the Camera

This report details a security analysis conducted on a network-connected **camera** and its companion mobile application. 
The assessment focused on identifying vulnerabilities in the device's setup process, network communication, and the mobile app's handling of user data.
While the camera's core functions demonstrated secure practices, the analysis revealed several weaknesses primarily tied to the mobile application.

---

### Key Findings

1. **Device Overview**:
   - The camera connects to a Wi-Fi network through the companion app, which allows users to monitor live footage, control motion,
   - and utilize features like two-way audio.
   - Additional functionalities include motion detection alerts, local video storage via MicroSD, and optional cloud storage.
   - The device's communication is heavily reliant on its mobile app, which manages most of the operations.

2. **Setup and Traffic Analysis**:
   - The device setup involves a QR code containing Wi-Fi credentials, transmitted in plaintext. This makes the credentials susceptible
   -  to interception during the setup process.
   - Traffic analysis revealed that video and audio streams from the camera to the cloud server are encrypted. However, some HTTP requests from
   - the app transmit user data, such as email addresses and device details, in plaintext.

3. **Application Vulnerabilities**:
   - The app’s implementation of TLS encryption has shortcomings, with gaps in SSL pinning that make it susceptible to man-in-the-middle
   - attacks in controlled environments.
   - Key vulnerabilities include:
     - Intercepted and modified HTTP requests allowed unauthorized changes, such as renaming the camera or granting access to additional users
     - without the owner's knowledge.
     - Sensitive data, like unique identifiers and API tokens, was exposed in unencrypted traffic.

4. **Security Strengths**:
   - Video and audio data transmitted by the camera were encrypted and sent via secure protocols, safeguarding against unauthorized access
   - to real-time footage.
   - TLS encryption was implemented for most server communications, ensuring data safety in typical scenarios.

---

### Recommendations

To improve the device's security:
1. **Secure the Setup Process**:
   - Encrypt Wi-Fi credentials in the QR code used during setup to prevent exposure.
2. **Enforce Complete Data Encryption**:
   - Mandate TLS encryption for all HTTP communications, especially user data and API requests.
3. **Enhance Application Security**:
   - Strengthen SSL pinning to prevent certificate forgery and unauthorized traffic interception.
4. **Harden API Requests**:
   - Introduce dynamic validation mechanisms for critical fields in API requests to mitigate replay and spoofing attacks.

---

### Conclusion

While the camera demonstrated secure practices in its core operations, vulnerabilities in its mobile app pose risks to user data and device
integrity. Addressing these gaps through encryption, secure communication protocols, and app security measures will significantly enhance the device's 
overall resilience against attacks.
