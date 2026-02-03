# CS471 – Lab 1: Internet Protocols Analysis using Wireshark

This lab demonstrates capturing and analyzing different Internet protocols using Wireshark.
The captured protocols include HTTP, HTTPS (TLS), TCP, and UDP (QUIC).
All traffic was captured from the Wi-Fi network interface.

---

## 1. UDP / QUIC Traffic Analysis (Video Streaming)

### Filter Used:
udp
![udp](https://github.com/user-attachments/assets/c48eb6bf-8995-407b-bebd-f9ab9e625c5e)

### Observation:
In this capture, the protocol shown is QUIC instead of plain UDP.
The packets use port 443 and the payload is marked as "Protected Payload".

### Explanation:
QUIC is a modern transport protocol that operates on top of UDP.
It is used by applications such as YouTube for video streaming.
Although the UDP filter is applied, Wireshark recognizes the higher-level protocol as QUIC.
The payload is encrypted, which is why the content is not readable.

### Reason for Appearance:
This traffic appeared because a YouTube video was playing during packet capture.
YouTube uses HTTP/3, which relies on QUIC over UDP to provide faster and more reliable streaming.

---

## 2. TCP and TLS (HTTPS) Traffic Analysis

### Filter Used:
tcp
![tcp](https://github.com/user-attachments/assets/105bd376-d518-42ef-91cb-758ea5a99e6e)

### Observation:
The capture shows TCP packets with TLSv1.2 and TLSv1.3.
Port 443 is used, and encrypted application data is visible.
TCP flags such as SYN, ACK are present.

### Explanation:
HTTPS uses TCP as its transport protocol.
TLS is responsible for encrypting the data exchanged between the client and the server.
Wireshark can show the handshake and encrypted packets, but not the actual content.

### Reason for Appearance:
This traffic appeared because secure websites (HTTPS) were accessed during the capture.
Modern web browsing relies on HTTPS to ensure confidentiality and data integrity.

---

## 3. HTTPS with TLS Handshake
![https](https://github.com/user-attachments/assets/b5883b42-6dd7-489a-8f32-655f7bbd0b0b)

### Filter Used:
tls

### Observation:
TLS handshake messages such as Client Hello and Server Hello are visible.
The packets indicate secure session establishment.

### Explanation:
TLS handshake is used to negotiate encryption parameters before secure data transmission.
This process ensures that communication is encrypted and secure.

### Reason for Appearance:
This traffic appeared because HTTPS websites were accessed.
Every secure connection starts with a TLS handshake.

---

## 4. HTTP Traffic Analysis (Unencrypted)
![http](https://github.com/user-attachments/assets/88354f40-fc0d-4050-9f38-45e1473f2241)

### Filter Used:
http

### Observation:
HTTP GET and POST requests are visible.
Status codes such as 200 OK and 304 Not Modified appear.
The data is readable in plain text.

### Explanation:
HTTP is an unencrypted protocol.
Wireshark can fully display request methods, URLs, and server responses.

### Reason for Appearance:
This traffic appeared because an HTTP website was accessed.
Unlike HTTPS, HTTP does not encrypt data, making it easy to analyze.

---

## Conclusion

This lab demonstrates how different protocols appear in Wireshark depending on the application and encryption method.
Modern applications prefer encrypted and high-performance protocols such as HTTPS and QUIC.
Wireshark is an effective tool for analyzing and understanding network communication behavior.
Sensitive information such as IP and MAC addresses has been masked for privacy.
