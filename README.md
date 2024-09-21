java c
INFO3616/CSEC3616/CSEC5616 — S2 2024 
Assignment - 2 
This is an individual assignment.
This assignment worths 10% of the final marks of the course and covers the content of Weeks 4-6 (inclusive).
Submit your final report as a PDF and codes as a zip file in Canvas. In Canvas, under Assign- ment 2, you will find two links to submit your report and code separately.
You should explain any details of how to run your code in the report.
Final Report and Code: Due by Week 5, Sunday the 22nd of September, 2024 11:59 PM*** IMPORTANT ***: In your answer sheet DO NOT repeat the questions. Simply include the question number and your answer only. If you include question text in your answer sheet, your TurnItIn score will be high and there will be additional checks. This will cause a delay in releasing your marks. We will also impose a penalty of 10% of the total marks. 
1 Breaking the Vigenère Cipher (20 marks) In the given zip file for Assignment 2, under Question 1 you will find a cipher text encrypted by the Vigenère cipher. Your task is to break it and find the original plain text. Please read the following instructions carefully.
• You need to write your own code for this. However, there will be some guesswork and analysis involved. So we do not expect your code to give the decrypted result straight away.  For example, if you are checking various substitutions, it is acceptable that you run your code multiple times to see which substitution results in a readable text.
• The spaces and punctuations such as . and ’ are not encrypted. You can store their positions into an array, remove them, do the decryption using your method, and insert them back to the correct positions in the final plaintext.
• You will need ideas from Kasiski  Test to break this.  However there can be other possible solutions. You are not allowed to use any online decryption tool to assist you.
• The key length is less than 20 characters and contain only capital English characters. It is a random string, not a meaningful word. The final plain text is readable and meaningful.
• In the report include a description of your approach, the key length, the key, and the final plaintext you obtained. Also, explain how your code works and how to run it so that the tutors can run your code.
2 Cipher Block Modes (20 marks) 
a) ECB vs. CBC With the ECB mode, if there is an error in a block of the transmitted ciphertext, only the corresponding plaintext block is affected. However, in the CBC mode, this error propagates. For example, an error in the transmitted C1 (in the CBC diagram in the lecture) obviously corrupts P1  and P2 .
i Are any blocks beyond P2  affected? (4 marks) 
ii  Suppose that there is a bit error in the source version of P1 .  Through how many ciphertext blocks is this error propagated? What is the effect at the receiver? (4 marks) Note: Here transmitted means the spatial aspect of cryptography.  i.e., the sender encrypts the message and sends it over a network and the receiver receives it. And then receiver decrypts it. As the network transmissions are not perfect, there can be transmission errors, e.g., bit flips in transmitted cipher text. When a transmitted cipher text block is corrputed due to tranmission error, the receiver may not be able to decrypt it to the correct plain text.
b) CBC-CTS (Cipher Block Chaining - Cipher Text Stealing) 
b) Read following description carefully about the CBC-CTS (Cipher Block Chaining - Cipher Text Stealing).Usually padding is done in block modes when the last block of plain text does not fill the block size. However, padding may not always be appropriate. For example, one might wish to store the encrypted data in the same memory buffer that originally contained the plaintext. In that case, the cipher text must be the same length as the original plaintext. CBC-CTS (Cipher Block Chaining - Cipher Text Stealing) is a block mode that creates cipher text exactly in the same length as the plain text. Figure 1 shows the overall operation of the scheme.
What is happening at the last two steps 
Assume that the last block of plaintext is only L bytes long, where L < block size. The encryption sequence is as follows:
1. Encrypt the first (N – 2) blocks using the traditional CBC technique.
2. XOR PN −1  with the previous cipher text block CN −2  to create YN −1 .
3. Encrypt YN −1  to create EN −1 .
4.  Select the first L bytes of EN −1  to create CN .
5.  Pad PN  with zeros at the end and XOR with EN −1  to create YN .
6. Encrypt YN  to create CN −1 .
7. The last two blocks of the cipher text are CN −1  and CN .
Now consider the following implementation of CBC-CTS
•  Block Length B is 4 bits
•  Key is 1101 and IV is 1001
• The plain text is 10101110001011
• The encryption function consists of two steps
– Using Figure 2 get the mapping (i.e., if plain text is x, the table gives F (x))
– XOR with the Key: Encrypted value E(x) is F (x) ⊕ K (i.e., E(x) = F (x) ⊕ K)

Figure 1: CBC-CTS block mode

Figure 2: Plaintext mapping as a table

Figure 3: CBC-CTS setup
Based on this information 
i  Complete the missing values in Figure 3.  Show your calculation steps. You may redraw the figure in your answer sheet. (8 marks) 
ii  Give the final cipher text. (4 marks)
3 RSA Calculation (20 marks) Suppose Bob is generating a public and private key pair using RSA algorithm. Bob choses the prime numbers p = 10007 and q = 53047.  He computed n = pq = 530841329 and ϕ(n) = (p − 1)(q − 1) = 530778276. He then chooses the encryption exponent e = 999983.
i Find the private key. i.e., d where ed ≡ 1  mod ϕ(n) using the Extended Euclidean algorithm (12 marks - 代 写INFO3616/CSEC3616/CSEC5616 — S2 2024 Assignment - 2Python
代做程序编程语言10 marks for the missing values in the table and 2 marks for d).
First follow the explanation below.
Recall the Euclidean Algorithm for finding the GCD or a and b. It goes like this
1) Calculate r1 = a  mod b which satisfies a = q1 b + r1
2) Calculate r2 = b  mod r1  which satisfies b = q2r1 + r2
3) Calculate r3 = r1   mod r2  which satisfies r1  = q3r2 + r3
...
i) Calculate ri  = ri−2   mod ri−1  which satisfies ri−2  = qiri−1 + ri
...
n) Calculate rn+1 = rn−1   mod rn  = 0 which satisfies rn−1  = q n+1rn + 0 When rn+1  becomes zero gcd(a, b) = rn
Next we assume that each step we can find xi  and yi  that satisfy ri  = axi  + by i. We end up with the following sequence.
a = q1 b + r1  and r1  = ax1 + by1   b = q2r1 + r2  and r2  = ax2 + by2  r1 = q3r2 + r3  and r3  = ax3 + by3
rn−2 = qnrn−1 + rn  and rn  = axn + by n rn−1 = q n+1rn + 0
We can rearrange the terms in above equations to obtainri = ri−2 − ri−1qi                                                                                    (1)
But we also know that ri−2  = axi−2 + by i−2  and ri−1  = axi−1 + by i−1By substituting in Equation (1) we get.
ri = (axi−2 + by i−2) − (axi−1 + by i−1)qi
ri = a(xi−2 − qixi−1) + b(yi−2) − qiyi−1)
Since we assumed ri = axi + by i  by co-efficient matching we can get
xi = xi−2 − qixi−1  and yi  = yi−2 − qiyi−1
Based on this information your task is to fill the blanks in Table 1 and provide the value of d.
Explain Step 2 in the Table in detail and the rest of the steps you can fill the table without describing it.
ii  Suppose Bob shared his public key e with Alice. If Alice wants to send the message 3 to Bob, find the encrypted message.  Show your steps of exponentiation by squaring (You don’t  have to show all the steps but you can show first 2-3 steps of the exponential squaring and  show the final answer - you can use an online calculator the find the final answer e.g. https: //www.dcode.fr/modular-exponentiation).  (4 marks).
Table 1: Computing the decryption exponent d. 

iii Verify that Bob can decrypt what Alice sends.  Describe the required computation and use an online calculator to obtain the final answer.  (4 marks).
4 Breaking RSA with Fermat’s Factorization (20 marks) Fermat’s factorization is a method for finding the factors of a composite number N by expressing it as the difference of two squares.  It can be particularly useful for breaking poorly configured RSA setups where the two prime factors p and q of N = p × q are close to each other.
Conduct your own research and learn about how Fermat’s Factorization works.
Example links Link 1, Link 2. In the given zip file for Assignment 2, under Question 3, you are given a n (modulus) and e (public key) of an RSA system. You are also given c (a cipher text) encrypted using e. Write a program and find the following. (4 marks for each) 
i Using Fermat’s Factorization method find the two prime factors of n, i.e., p and q in the RSA notation.
ii Find ϕ(n).
iii Find the private key d.
iv Find the corresponding plaintext p for the given c as an integer.
v  Convert the decimal to ASCII and find the readable (and also meaningful) plain text. For this step, convert the integer into binary, read 8-bits at a time and convert them to the ASCII character using the chr function.
• The correct plaintext in binary should have 160 bits. That is 20 ASCII characters.
•  Python will not add leading zeros when you convert decimals to binary. So if you get a binary string of 159 bits, simply add a leading bit 0. Otherwise you might not be able to decode it in ASCII code.
In the report include the answer to above questions and explain how your code works. Submit your code in the seperate link given in Canvas.
As you are dealing with large numbers use the Python library gmpy2 and the mpz format to represent large integers.
5 Message Authentication Codes (20 marks) 
a) Message Authentication Codes vs. Hashes 
i Explain what a message authentication code is. (2 marks) 
ii  Explain the difference between a message authentication code and a one-way hash function. (2 marks) 
b) A Simple Message Authentication Code Alice wants to send a single bit of information (a yes or a no) to Bob by means of a word of length 2. Alice and Bob have four possible keys available to perform. message authentication. The matrix in Figure 4 shows the 2-bit word sent for each message under each key:
i The preceding matrix is in a useful form. for Alice. Construct a matrix with the same information that would be more useful for Bob. (4 marks) 
ii What is the probability that someone else can successfully impersonate Alice? (2 marks) 
iii What is the probability that someone can replace an intercepted message with another message successfully? (2 marks) 

Figure 4: A simple message authentication code.
c) Authenticated Encryption (AE) 
In the lecture (and also in the textbook) we discussed four approaches for Authenticated Encryption (AE). They are:
• Hashing followed by encryption: i.e., send Enck(m, H(m))
• Authentication followed by encryption (MAC-then-encrypt): i.e., send Enck1 (m, MACk2 (m))
• Encryption followed by authentication (encrypt-then-MAC): i.e., send Enck1 (m), MACk2 (Enck1 (m))
• Independently encrypt and authenticate (MAC-and-encrypt): i.e., send Enck1 (m), MACk2 (m)
Based on those four scenarios answer the following questions.
i Which of the above performs decryption before verification. Explain your answer. (4 marks) 
ii Which of the above performs verification before decryption. Explain your answer. (4 marks) 









         
加QQ：99515681  WX：codinghelp
