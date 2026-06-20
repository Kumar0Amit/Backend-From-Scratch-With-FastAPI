# Questions.md

# Module 1 – Internet Fundamentals

## 1.1 History of the Internet

### Concept Questions

1. What was ARPANET?
2. Why was ARPANET created?
3. Who funded ARPANET?
4. What problems did ARPANET try to solve?
5. What was the first message sent over ARPANET?
6. How did ARPANET evolve into today's Internet?
7. Why are common protocols necessary for connecting different networks?

### Why Questions

8. Why couldn't early computers communicate easily?
9. Why was reliability an important requirement during the Cold War?
10. Why is packet switching better suited for the Internet than circuit switching?
11. Why does the Internet not rely on one fixed communication path?

### Comparison Questions

12. Explain Packet Switching.
13. Explain Circuit Switching.
14. Compare Packet Switching and Circuit Switching.
15. Give one real-world example where Circuit Switching is preferable.
16. Give one real-world example where Packet Switching is preferable.

---

## 1.2 What is the Internet?

### Concept Questions

17. Define the Internet.
18. Why is the Internet called a "Network of Networks"?
19. What is a network?
20. What is distributed communication?
21. What is global infrastructure?
22. What is a Local Area Network (LAN)?

### Why Questions

23. Why isn't the Internet one giant centralized network?
24. Why is distributed communication more reliable?
25. Why are fiber optic cables important?
26. Why do we need Internet Service Providers (ISPs)?

### Comparison Questions

27. Internet vs Local Network.
28. Internet vs World Wide Web.
29. Explain why the Web is only one service running on the Internet.

### Scenario Questions

30. Describe the journey of a request from your laptop to Google's servers.
31. What role does your ISP play when you open a website?

---

## 1.3 How Computers Communicate

### Concept Questions

32. How do computers communicate?
33. What is a message?
34. What is data transmission?
35. What is a sender?
36. What is a receiver?
37. What is standardization?

### Why Questions

38. Why can't computers communicate without rules?
39. Why is standardization necessary?
40. Why is data divided into packets?

### Scenario Questions

41. Explain what happens when you open YouTube.
42. Explain how a login request travels from your laptop to a server.
43. What problems would occur if every company invented its own communication language?

---

## 1.4 Protocols

### Concept Questions

44. What is a protocol?
45. Why do protocols exist?
46. What is a protocol stack?
47. What is the Application Layer?
48. What is the Transport Layer?
49. What is the Internet Layer?
50. What is the Network Access Layer?

### Protocol Questions

51. What is HTTP?
52. What is HTTPS?
53. What is TCP?
54. What is UDP?
55. What is DNS?
56. What is FTP?
57. What is SMTP?

### Comparison Questions

58. HTTP vs HTTPS.
59. TCP vs UDP.
60. FTP vs SMTP.

### Why Questions

61. Why is HTTPS more secure than HTTP?
62. Why is TCP used for websites?
63. Why is UDP preferred for online gaming?
64. Why do we need DNS?

### Scenario Questions

65. Explain what happens internally when you type `google.com` into your browser.

---

# Module 2 – Client–Server Architecture

## 2.1 What is a Client?

### Concept Questions

66. Define a client.
67. What are the responsibilities of a client?
68. Can a Python script be a client?
69. Can a backend service be a client?
70. Can an IoT device be a client?

### Why Questions

71. Why does the client initiate communication?
72. Why is the browser considered a client?
73. Can one device act as both a client and a server? Explain.

---

## 2.2 What is a Server?

### Concept Questions

74. Define a server.
75. What are the responsibilities of a server?
76. What is the listening state?
77. Why does a server spend most of its time waiting?
78. What happens after a request reaches the server?

### Why Questions

79. Why doesn't a server usually initiate communication?
80. Why can one server handle multiple clients?

---

## 2.3 Client–Server Communication

### Concept Questions

81. What is a request?
82. What is a response?
83. What is stateless communication?
84. What information can a request contain?
85. What information can a response contain?

### Scenario Questions

86. Explain the request-response cycle using a login example.
87. Explain the request-response cycle using a Google search.
88. Explain why HTTP is called stateless.
89. If HTTP is stateless, how do websites remember users?

---

# Module 3 – Backend Engineering

## 3.1 Where Does Backend Fit?

### Concept Questions

90. Where does the backend fit in a web application?
91. What is the frontend?
92. What is the backend?
93. What is the database?
94. What is infrastructure?
95. What is a web server?
96. What is an application server?

### Comparison Questions

97. Frontend vs Backend.
98. Web Server vs Application Server.

### Why Questions

99. Why shouldn't the frontend communicate directly with the database?
100. Why do we separate frontend, backend, and database?

---

## 3.2 Responsibilities of Backend

### Concept Questions

101. What is business logic?
102. What is authentication?
103. What is authorization?
104. What is validation?
105. Why does the backend communicate with the database?
106. What is an API response?
107. Why is error handling important?

### Comparison Questions

108. Authentication vs Authorization.

### Scenario Questions

109. Explain what happens when a user clicks "Buy Now."
110. Explain the backend workflow for a login request.
111. Explain why validation is important.

---

## 3.3 What Backend Does NOT Do

### Concept Questions

112. Does the backend perform DNS resolution?
113. Does the backend establish TCP connections?
114. Does the backend perform TLS handshakes?
115. Does the backend render HTML?
116. Does the backend control Internet routing?

### Why Questions

117. Why doesn't the backend handle browser rendering?
118. Why isn't DNS part of backend logic?
119. Why is TLS usually handled by a web server or reverse proxy?

---

# Module 4 – Journey of a Request

### Concept Questions

120. Explain the complete journey of a request from the browser to the database and back.
121. What role does DNS play?
122. What role does TCP play?
123. What role does TLS play?
124. What role does the Web Server play?
125. What role does the Application Server play?
126. What role does the Backend play?
127. What role does the Database play?

### Challenge Questions

128. Explain the complete request lifecycle without looking at your notes.

---

# Module 5 – Browser Basics

### Concept Questions

129. What is a browser?
130. What are the responsibilities of a browser?
131. What is the Address Bar?
132. What is the Browser Engine?
133. What is the Networking Layer?
134. What are Developer Tools?
135. What is the Network Tab?

### Scenario Questions

136. How would you debug an API that isn't returning data using the Network Tab?
137. Explain what happens after pressing Enter in the Address Bar.

---

# Module 6 – Development Environment

### Concept Questions

138. What is a development environment?
139. What is local development?
140. What is localhost?
141. What is 127.0.0.1?
142. What is a port?

### Comparison Questions

143. localhost vs 127.0.0.1.
144. Development vs Production.

### Why Questions

145. Why do developers use localhost?
146. Why are ports necessary?
147. Why don't developers build applications directly on production servers?

---

# Revision Challenge

Without looking at your notes, explain the following from memory:

1. How the Internet evolved from ARPANET.
2. What happens when you type a URL into your browser.
3. How two computers communicate over the Internet.
4. The complete request-response lifecycle.
5. The responsibilities of a client.
6. The responsibilities of a server.
7. The responsibilities of the backend.
8. The complete architecture of a modern web application.
9. The role of each protocol: HTTP, HTTPS, TCP, UDP, DNS, FTP, SMTP.
10. The complete journey of a request from the browser to the database and back.
11. Why localhost exists and how local development works.
