---
layout: base
title: Kevin’s Biweekly Tech Digest - No.001
permalink: kevin_digest_001.html
---

Welcome to my first installment of Kevin's biweekly digest. As they say, "sharing is caring" and as a team we should care about the tools, tech and practices we use
to get the job done. So to show I care I am sharing exactly that, all the tools, technologies, best practices and research topics I have explored and continue to 
discover on this wonderful adventure they call software development. Hopefully, these digests will have you opening browser tabs at a rate of knots, as we
navigate interesting topics together (please don't @me about your system resources).

## Best Practice

This week in best practice, Architectural Decision Record (ADR) because a ~~stitch~~ document in time saves nine. Have you ever read a codebase and wondered why they made that decision? Why was a particular library, design pattern, algorithm or tech-stack used? Then, when asked by a new start or someone unfamiliar with the codebase you search through your emails for *that* thread where you and the team hashed it out and came to an agreement. This is a common situation and... it's an anti-pattern, the 'Email-Driven Architecture' anti-pattern. I want to shout from the rooftops "an email is not an appropriate document store". Like it or not, communities create cultures and cultures have tacit knowledge that may or may not be shared. Explicitly stating why an important architectural decision was made, in a centralised place, can be an invaluable source of knowledge for those who come to the codebase after the decisions have been made. A caveat, I have also come to appreciate that shared documentation does not necessarily mean shared knowledge and that conversations are essential for good documentation. 

An ADR is a short plaintext document communicating architectural decisions. The ADR was first proposed by Michael Nygard and his template can be found on 
[github](https://github.com/joelparkerhenderson/architecture-decision-record/blob/main/templates/decision-record-template-by-michael-nygard/index.md). You can read more about ADRs [here](https://github.com/joelparkerhenderson/architecture-decision-record).

The ADR captures the scope of the decision by providing a:

- Title	- An appropriate title captures the intent of the ADR, the essential nature of the decision should be captured. As an example, "**Use a bash script for configuration and installation**".
  
- Status - The status reflects the condition of the ADR, for example: proposed; accepted; rejected; or deprecated.
  
- Context - Providing information motivating the decision and its significance captures the context.
  
- Decision - A description of the change proposed, making explicit the proposition or work being undertaken.
 
- Consequences - As a result, what becomes easier based on the proposed change?

The ADRs can be kept in your code repository under a speperate directory structure. Interestingly, there is also a command line tool that will assist you in creating and maintaining an ADR called [adr-tools](https://github.com/npryce/adr-tools). However, you can always just fire up a terminal and use your favourite text editor (insert [editor wars](https://en.wikipedia.org/wiki/Editor_war) here) to write one in markdown. 

## Technology of the week

To json or not to json, is that even a question? We are lucky, we have choices and when it comes to picking the right tool for the job in a tech stack there are always
alternative options with different trade-offs. So here too we find options when serialising data for interoperability and communication between endpoints. 

Json and gRPC are two diffrent technologies that can be used to implement RESTful APIs. Where once XML was the standard json now reigns supreme. However, gRPC 
is an alternative inter-process communication technology, using a binary based messsage protocol instead of clear text. gRPC also uses an 
interface definition language (IDL) for defining the interface that allows for cross-language communuication. The IDL is provided by Google's protocol buffers (protobuf)
framework for serialising structured data. There are several benefits to using gRPC:

- Clear endpoint design.
- Two way communication allows remote procedure invocation (RPI) and messaging style communication
- Interoperability between language agnostic clients and servers

The protobuf library can be found on [GitHub](https://github.com/protocolbuffers/protobuf) and more details on how to use the library can be found in [Google's Documentation](https://developers.google.com/protocol-buffers/). The only thing left to ask is... Are you gRPC'ing what I am saying...sorry I couldn't resist. 


## Algorithm of the week

I think the general theme of this digest has been around sharing so, inkeeping with that theme, what do you do when you want to share something in secret?
Well, we could use a cipher. A cipher substitutes plaintext characters (usually individual or pairs) with other characters using a consistent rule. 
One of the most famous ciphers in history is the Ceasar cipher. The application of the cipher is as follows:

- Take the 26 letter alphabet and represent a...z with 1-26 
- Encode your message by taking the plaintext characters from your original message, and replace the characters with a character plus three away
- Wrap around after 26 and strting from 1 again for x, y and z.

Following the rules we can convert the plaintext message into ciphertext, rendering "the big secret is xyz" as "wkh elj vhfuhw lv abc".

This system is represented formally in mathematics by modular arithmetic and the number we "wrap around" is called the modulus. The character 'x' in the Ceasar cipher can be represented by:

\begin{align}
	24 + 3\equiv 1 \text{ mod } 26
\end{align}

Lovely, but hold up! There are a few issues with this system.

1. The same words in plaintext always form the same ciphertext.
2. The secret key/operation "plus three" needs to be communicated in advance without anyone else intercepting the communication.
3. Once the system is broken every message ever sent is now decipherable.

Point one is of significance because, human languages have a grammatical structure and the frequency of characters can identify words. For example connective words
 are strewn through sentences and paragraphs. Eventually the frequency will give away substitute characters for common words 
and subsequently reveal other words and break the code. Point two and three require a lot of planning to prevent. 

So, what happens when we cannot meet to agree the key or gaurantee the confidentiality of our meeting.
We need a way to share the key without pre-arranging the exchange and in a manner that makes it improbable that a third party intercepts the key. Asymmetric keys are 
based on number theory and their ciphers are built around the requirement to solve a mathematical problem that is known to be hard like 
factorisation and discrete logarithms. The logic behind their use is quite simply that they are known hard problems that a lot of people have tried to solve and have 
failed.

RSA is a public key encryption scheme and, for a long time, has been an important standard in the security of the internet. At the heart of RSA is 
integer factorisation, mapping:

\begin{align}
	f : x \rightarrow x^{e}\mod n
\end{align}

The [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) algorithm was created by [Ron Rivest](https://en.wikipedia.org/wiki/Ron_Rivest), 
[Adi Shamir](https://en.wikipedia.org/wiki/Adi_Shamir) and [Leonard Adleman](https://en.wikipedia.org/wiki/Leonard_Adleman). 
The first letters of their surnames forming the initialism RSA.

For RSA, the method of encryption is not a mapping of characters to their index value with an arbitrary rule set for the key as in the Ceasar cipher. Instead, RSA 
uses the modulus $$N$$ and private exponent $$e$$ as the encryption key, and a public exponent $$d$$ as a decryption key. 
A large value for $$N$$ is hard to factor and as such will provide a way to cipher the text with a private key. 

Let's go through an example together using smaller numbers for illustration:

- First we generate two prime numbers $$p$$ and $$q$$, such that $$p\neq q$$. Typically large prime numbers ($$\geq 1028$$ bits) are used. 
In this example we will use, $$p=11$$ and $$q=17$$

-  We calculate $$N=pq$$:

\begin{align}
	11\times 17=187
\end{align}

- We calculate PHI $$\phi = (p-1)(q-1)$$. So for our example:

\begin{align}
	\phi = (11-1)(17-1) = 160
\end{align}

- We select a value for the private exponent $$e$$ ensuring no common factors with PHI and $$1<e<\phi$$. 
The value of $$e$$ in practice is always known and is $$010001$$ in binary or 65,537. We will use $$e=3$$.

- Now we have our encryption key $$E(e, N)$$

- To create a decryption key we need the public exponent $$d$$ such that $$ed \equiv 1$$ mod $$\phi$$ and $$1<d<\phi$$

\begin{align}
	d = e^{-1} \text{ mod } \phi 
\end{align}	

So:

\begin{align}
	d= 3^{-1} \text{ mod } 160 = 107 
\end{align}

- Now we have our decryption key $$D(d,N)$$
- We take a message M, lets say I want to share how many cups of coffee I drink a week M=9.To cipher the message we:

\begin{align}
	Cipher=M^{e}\mod N
\end{align}

so our message becomes:

\begin{align}
	C = 9^{3}\mod 187 = 168
\end{align}

Now when the recipent of the message receives 168, they may think "wow he loves coffee", and I do but who drinks 168 cups a week? 

- The message needs to be decrypted using the decryption key:

\begin{align}
	Decipher = C^{d} mod N
\end{align}

So, to retrieve the message where I divulge my weekly coffee consumption, we rasie the cipher value to the public exponent $$d$$ mod $$N$$:

\begin{align}
	D = 168^{107} \mod 187  = 9
\end{align}

Now, my true coffee count is revealed. How the algorithm is used in public key encryption is beyond the scope of the algorithm of the week section. However, if you
would like to read more about public key encryption and key exchange, then please checkout the book recommendation and urls at the end of this digest.

## Books Recommendations

| Title  | Author | ISBN |
|:-------|:-------|:-----|
| Fundamentals of Software Architecture | Mark Richards and Neal Ford | 978-1492043454 |
| The Mathematics of Secrets | Joshua Holden | 978-0691183312 |
| Security Engineering | Ross Anderson | 978-1119642787 |


## Useful Websites 

[asecuritysite-rsa](https://asecuritysite.com/rsa/rsa)


## Useful Youtube Videos

[RSA with Professor Bill Buchanan OBE](https://www.youtube.com/watch?v=0zArGECThXI&t=893s)
