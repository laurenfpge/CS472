Lauren Gumiit lfg34

## Part 1:
| Problem | Solution/Not Addressed | How We See This Today |
|---------|------------------------|-----------------------|
| Reliability Across Multiple Networks: How do you ensure data gets through when it has to cross several different networks? | To ensure data gets through several networks, the paper proposes multiple ways to keep track of the traveling data. For example, having the receiver send back an acknowledgement to show data has been received. They also add the functionality of fragmentation to support multiple networks. Lastly, we also mark the ends of segments and messages to ensure the entire message is received. | When I send messages to family members over seas,  I can be sure that they have received the message. Sometimes when I send multiple messages, on my end, it looks like they might have sent out of order but based on responses I can tell the message was received correctly. |
| Addressing Across Networks: How do you create addresses that work across different network types? | The idea of addresses was to have a uniform internetwork address that each gateway and TCP could understand. They chose a network ID of 8 bits and using different parts of the address to mark a destination network and gateway. | By doing any type of work that utilizes the internet, I can see that my data is being transmitted successfully. Whether it is streaming content, sending messages, or online shopping, I am interacting without issue.  |
| Accounting/Billing: How do you handle charging when data crosses networks owned by different organizations? | The paper assumes that each network charges a fixed rate per packet transmitted and that an increase in a network’s packet size does not result in an additional cost, making the cost to the user almost constant. | I think that we see the opposite today. Where different companies make users pay more for more reliable, fast, and large internet usage. We can see this in applications like streaming services or cloud storage. | 
|Routing Between Networks: How does data find its way from Network A through Network B to reach Network C? | The paper traces the flow of data in Figure 2. To send data from process X to process Y, it enters and traverses network A. At the gateway the packet is then reformatted to be able to traverse network B. This is repeated until the destination is reached. | When I using shopping services originating in other countries like Korea, I can still interact with the website like normal. Despite the physical distance, the data and connection is still reaching its destination. |
| Privacy/Encryption: How do you prevent others from reading your data as it crosses multiple networks? | The paper did not talk about ensuring privacy and security between the user and product. | As users we typically trust the website or platform that our data is protected. Especially with messaging systems, we cannot be sure that the inbetween networks are not reading out data. | 
| Network Performance at Scale: What happens when millions of people try to use the internet simultaneously? | The paper does not address how to handle large traffic. While they had ideas on how to handle the growth of the internet, they did not address the management of millions of users. | With so many people staying connected to the internet constantly, we often see latency and delays. |

## Part 2:
### Section A:
Problem - (row 5) "How do you prevent others from reading your data as it crosses multiple networks?"

Specific Scenario - How can I be sure that my data is private from other networks when I send messages on online platforms like Slack or GroupMe? Is it similar to the proposed ideas in Cerf-Kahn's paper?

### Section B:
1. I am trying learn about the inner workings of the internet. Specifically, I'm investigating: "(Privacy/Encryption) How do you prevent others from reading your data as it crosses multiple networks?" Specifically, for the platform Slack because I know many organizations use it to communicate within their company. How can they be sure that the messages stay private.
2. So the metadata is the encrypted version of the message? I know there are encryption keys, but for Slack how difficult is it to decrypt the message when you aren't the intended recipient.
3. Do different companies have different strengths of encryption? Do they pay more to have stronger protection? Is it possible to have stronger and weaker encryption?
4. In relation with Cerf-Kahn's 1974 paper "A Protocol for Packet Network Intercommunication" I know they do not talk about privacy in the internetwork, but do these encrypted messages and data travel the network like every other message? It is kinda like putting a mask on the message?

### Section C:
In my conversation with AI, I was curious about how data is protected as it traverses multiple networks and while the Cerf-Kahn paper did not address this I learned that the data travels like any other data. I specifically asked about how messages sent within Slack stay private. I learned that the message is encrypted before it hits the network, but it is treated like any other packet. The universal address is still used and is not encrypted, and the packet is still broken up into smaller packets to ease with traveling over different networks. Once it has reached its destination, the message is then decrypted like any other. In terms of the internetwork system, I also learned that modern networks do not use the original proposed ES/EM signaling concepted and instead use packet forwarding inside routers and switches, but this does not change when dealing with the encrypted messages.  

### Section D:
I also learned how companies differ in terms of encryption, specifically how major companies and platforms have an industry-standard encryption that is stronger than other encryption methods. Stronger encryption typically means more complicated algorithms and longer key lengths. I had thought that companies simply paid more for stronger security, but the money mainly goes towards the ability to manage their own encryption keys, keeping data in specific countries, and more frequent key rotations. It was surprising to learn that most platforms use the same encryptions, but usually pay for more control over the management of the application of the encryption and access to keys.

### Section E:
**ME:** I am trying learn about the inner workings of the internet. Specifically, I'm investigating: "(Privacy/Encryption) How do you prevent others from reading your data as it crosses multiple networks?" Specifically, for the platform Slack because I know many organizations use it to communicate within their company. How can they be sure that the messages stay private?

**AI:** [ Great question—this gets right to the heart of how privacy works on the modern internet. 
I’ll explain this in layers, starting with how data is protected as it travels across the internet, then how Slack specifically handles message privacy, and finally what “private” really means in practice. 

1. The core problem: data crossing many networks 
When you send a Slack message, it doesn’t go directly from your laptop to your coworker’s laptop. It travels through: 
Your device → Wi‑Fi/router
Your ISP 
Multiple intermediate networks (backbone providers, data centers) 
Slack’s servers 
Then the same process in reverse to the recipient 
Any of these networks could inspect or copy the data unless it’s encrypted. 
So the fundamental solution is: 
Encrypt the data so that only the intended parties can read it 
 
2. Encryption in transit: how others are prevented from reading your data 
TLS (Transport Layer Security) 
Slack (like most modern services) uses TLS, the same technology behind HTTPS. 
When your Slack app or browser connects to Slack: 
TLS handshake 
Your device verifies it’s really talking to Slack (via certificates). 
A shared session key is securely negotiated. 
Encrypted channel 
All messages are encrypted before leaving your device. 
Routers and ISPs only see: 
Source and destination IPs 
Encrypted blobs of data (not message contents) 
Decryption only at Slack 
Only Slack’s servers have the session keys needed to decrypt the data. 
What attackers can and cannot see

| Observer | Can see content? | Can see metadata? |
|----------|------------------|-------------------|
| Wi‑Fi owner | ❌ No | ✅ Yes |
| ISP | ❌ No | ✅ Yes |
| Network attackers | ❌ No | Limited |
| Slack | ✅ Yes | ✅ Yes 

So encryption prevents eavesdropping, but not visibility by Slack itself. ]

**ME:** So the metadata is the encrypted version of the message? I know there are encryption keys, but for Slack how difficult is it to decrypt the message when you aren't the intended recipient.

**AI:** [ Good instincts—this is exactly where people often get tripped up. Let’s clarify a couple of key concepts and then answer your “how hard is it to decrypt?” question precisely. 

1. First correction: metadata ≠ encrypted message 
Metadata is not the encrypted version of the message. 
They are two different things: 
Message content 
The actual text you typed 
This is encrypted during transit (TLS) 
Looks like random bytes while traveling over the network 
Metadata 
Information about the message, not the message itself 
Usually not encrypted end‑to‑end, though it may be protected by TLS in transit 
Typical Slack metadata includes: 
Who sent the message 
Who received it (channel, DM) 
Timestamp 
Workspace ID 
Message size 
IP address / device info (in some cases) 
Even when the content is encrypted, metadata often remains visible to the service provider (and sometimes network observers). 
Analogy: 
An envelope: 
Letter inside = encrypted message content 
Address, postmark, sender = metadata 

3. “How hard is it to decrypt the message if you aren’t the intended recipient?” 
This depends entirely on who you are. 
Case A: Random network observer (Wi‑Fi snooper, ISP, attacker) 
Difficulty: effectively impossible 
Why: 
TLS uses strong modern cryptography (e.g., AES‑128/256, ECDHE) 
Session keys are: 
Random 
Ephemeral (short‑lived) 
Never transmitted in plaintext 
To decrypt the message, an attacker would need: 
The session key or 
Slack’s private TLS key and a broken key exchange 
This would require: 
Breaking modern cryptography or 
Compromising Slack’s servers 
For practical purposes: 
It’s computationally infeasible with today’s technology. ]

**ME:** Do different companies have different strengths of encryption? Do they pay more to have stronger protection? Is it possible to have stronger and weaker encryption? 

**AI:** [ Absolutely—there can be differences in encryption strength, and it’s worth breaking down carefully. Let’s go step by step. 

1. What “stronger” and “weaker” encryption actually means 
Encryption strength isn’t about how much you “pay” per se; it’s about key length, algorithm choice, and implementation. 
Key factors

| Factor | How it affects strength |
|--------|-------------------------|
| Algorithm | AES, ChaCha20, RSA, etc. Some are stronger, some are outdated (e.g., DES is weak today). |
| Key length | Longer keys → exponentially harder to brute-force. Example: AES‑128 vs AES‑256. |
| Mode of operation | How encryption is applied (CBC, GCM, etc.). Some modes have vulnerabilities. |
| Implementation | Even strong algorithms are weak if implemented poorly (think side-channel attacks, padding bugs). |

Stronger encryption = modern algorithm + long keys + secure implementation. 
Weaker encryption = short keys, outdated algorithms, or buggy implementation. 

3. Do different companies have different encryption strengths? 
Yes, but in practice: 
Major platforms like Slack, Google, Microsoft, Zoom, etc. all use industry-standard TLS and AES encryption. 
Differences are usually subtle: 
Some might use AES‑256 vs AES‑128 (AES‑256 is stronger, though AES‑128 is already extremely secure). 
Some enterprise products let you use customer-managed keys, which can give an extra layer of control. 
Some companies may still support older protocols (TLS 1.0 or weak cipher suites), which is weaker. 
Reality: For a normal user, all major SaaS providers are already very hard to attack cryptographically. The “strength” differences mostly matter for nation-state attackers or highly sensitive environments. ]

**ME:** In relation with Cerf-Kahn's 1974 paper "A Protocol for Packet Network Intercommunication" I know they do not talk about privacy in the internetwork, but do these encrypted messages and data travel the network like every other message? It is kinda like putting a mask on the message?
**AI:** [ Exactly! That’s a very good way to think about it, and yes—it ties nicely back to Cerf and Kahn’s 1974 paper. Let’s unpack this carefully. 

1. Cerf-Kahn 1974: The foundation 
In their seminal paper: 
They describe a protocol for interconnecting different packet-switched networks (the birth of TCP/IP). 
Key points: 
Messages are broken into packets. 
Each packet has a header (routing information) and a payload (the actual data). 
The network doesn’t care what’s in the payload; it just routes packets. 
No consideration for privacy or encryption—the assumption was that anyone on the network could read the payload. 

2. Where encryption fits in today 
Fast-forward to modern networks: 
Encryption happens before the data hits the network. 
TLS (for web, Slack, email) and other protocols wrap the payload in a cryptographic “mask.” 
The network still treats the encrypted data exactly the same as normal packets. 
Analogy: 

| Concept | Analogy | Notes |
|---------|---------|-------|
|Original Cerf-Kahn packet | Letter in an envelope | Anyone handling it can read the letter |
| Encrypted message | Letter in a sealed, tamper-proof envelope | The network sees the envelope and address, but not the letter |
| Network routers | Postal system | Just forward packets; never open envelope |
| TLS session key | The secret code to unlock the envelope | Only sender and server can read the letter |

So yes—it travels the network like every other message. Encryption just “masks” the content so the intermediaries cannot read it. ]

## Part 3:
Before reading this paper I had no insight on the inner workings of the internet. I was surprised that this paper had been written in 1974 and had very well-thought propositions as to how the internetwork could work. I was also surpised that there was no mention of the privacy and security of packets as they are being sent across the internetwork. I feel like that would also be a big part of the conversation but I think the current system makes sense. Encrypting the data before it is sent over the network and treating like any other packet, is much more efficient rather than having a complete different system. AI taught me of this process and how, in a way, it stays true to what Cerf-Kahn proposed regarding the internetwork system. Honestly, I had no prior understanding of how the internet works, so reading this paper gave me background to better understand the modern implementation. I learned how packets traverse multiple networks and send different signals to ensure that the message can be rebuilt after fragmentation.  




































