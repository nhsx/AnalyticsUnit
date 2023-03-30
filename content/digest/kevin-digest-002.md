---
layout: base
title: Kevin’s Biweekly Tech Digest - No.002
permalink: kevin_digest_002.html
---

Welcome back for another instalment of Kevin's biweekly tech digest. This week in best practice, we cover unit testing. In technology of the week we cover Podman 
an alternative to Docker and in algorithm of the week, we look at key exchange with the Diffie-Hellman algorithm.

## Best practice

If you have ever written code, then you have written a bug. Opening sentence and shots fired, although, this really should not be a controversial statement. 
I have and I suspect you have too, so what steps can we take to verify our code is trustworthy? Writing idiomatic code helps and makes it easier for us and for others, 
following the generally accepted conventions of your chosen language and software engineering, to read and fix the code. However, when all is said and done, 
unit testing can assist you in ensuring you have sustainably updatable code that is trustworthy.  

A unit test is defined as an automated test that verifies a small piece of code in isolation. Better software design, is not the goal of unit testing. 
Unit test help to fight software entropy, reduce technical debt and maintain the quality of your code as you extend and improve the codebase. 
Inadvertently, the process of writing good unit tests may highlight where the code is difficult to isolate and test, indirectly pushing for better software design.
Unit tests provide fast feedback when updating code, however being able to test code does not mean the code or the tests are well-written. 
Production code and test code are both still code and as such passing tests must also be maintained when changes are made to the code, infrastructure or 
upstream dependencies. The diagnostic power of tests reduces when tests are not maintained increasing the chance of a serious regression (bug). 
Unit testing must be adopted as part of a general engineering culture, with continuous integration / continuous deployment (CI/CD) 
tools to assist in automating and monitoring test suites and help triage points of failure.

At the heart of a unit test is a unit of code. So, what is a unit of code? An isolated block of code --simples. Well, you will not be surprised to 
know that there are two schools of thought on what constitutes a unit of code, the 'classical' and 'mockist' school. The two schools differ on the:

- Definition of a unit
- Requisite level of isolation of code
- Handling dependencies

The mockist school requires the isolation of classes from all other dependencies and any required behaviour encapsulated by the omitted 
dependencies must be mocked (:bell: shame!) using a simplified imitation. The logic behind using mocks and testing only the system 
being developed is that any resulting failure can only come from the code under test. The classical school uses the 'Arrange', 'Act', and 'Assert' and
does not require the decoupling of interdependencies between object. If a test fails in the classical school, it is possible that the failure 
has been propagated from elsewhere in the code and not directly from the code under test.

### Coverage

Armed with what a unit is, how do we know how much of the codebase is covered? 
A coverage metric is used to indicate the code covered by the unit test suite. The coverage, represented as a percentage, 
does not convey the quality of the test coverage. With that in mind, aiming for a specific percentage of coverage is not a great idea. 
While a lack of tests is a good indication that "there be dragons" in the code, a project with a lot of tests does not promise a dragon free experience. 
The moral of the story is a test suite with 100% coverage can still be [toothless](https://www.dreamworks.com/how-to-train-your-dragon/explore/toothless).
A typical ratio for production code to test code can be between 1:1 and 1:3 lines. However many lines, there are two ways of calculating coverage:

1. Code Coverage:

	\begin{align}
		\text{Code coverage } = \frac{\text{Lines of code executed}}{\text{Total number of lines}}
        \end{align}

2. Branch Coverage:

	\begin{align}
		\text{Branch coverage } = \frac{\text{Branches traversed}}{\text{Total number of branches}}
	\end{align}

Code/Test coverage indicates how much of the production codebase is executed by at least one test.This test coverage metric is the most popular. 
The branch coverage focusses on how many branches of the codebase's control logic (IF, FOR, SWITCH etc) are covered. 
Increasing the number of lines of code in a test will not increase the coverage, if a code branch is continuously ignored.
 
## Technology of the week

:studio_microphone: :notes: "Setting Docker up at my cubicle bay, watching my aaaapp abstract away" :notes:. I think that is how Otis Redding meant to sing that 
[song](https://www.youtube.com/watch?v=rTVjnBo96Ug). I wonder if Otis knew about alternatives to Docker? At this point, containerisation and Docker are synonymous.
A bit like Google being the last name in search. I frequently say "Google it!", when I mean search the web for an answer. "Bing it" is pithy but I guess it has 
not caught on. Ten points if you can come up with something for DuckDuckGo..."Duck it". Docker is not the final name in containerisation.
It was not even the first engine to utilise the features available in the Linux kernel ([LXC](https://linuxcontainers.org)) although, arguably, 
it may be the most prolific container engine. Container technology has an interesting history from FreeBSD jails, Solaris Zones to LXC. 

Containerisation is the technology of the week but specifically [Podman](https://podman.io), a popular alternative to Docker. Why? 
Well, as we champion open ways of working and open source we have to accept that sometimes technologies that start off open and free can, 
in their search for revenue to sustain the project, become more restrictive and expensive.
I am not going to argue about the ethics around pursuing revenue for open source projects and 
I do not necessarily think it is a deal breaker --devs have to eat ~~langoustines~~ too. If alternatives exist then they should be on our 
[radar](https://www.thoughtworks.com/en-gb/radar).

Podman is a containerisation engine from RedHat and is almost at feature parity with Docker with the addition of a notable improvement. Podman uses rootless containers 
which are more secure, and allow non root users to start containers with restricted privileges.                                                                                                                               
### Installing and using Podman on macOS

Podman is available on macOS via the Homebrew package manager.

```bash
    $ brew install podman
```

Now you can create and start your first Podman machine using:

```bash
    $ podman machine init
    $ podman machine start
```

To use Podman in place of Docker, on a macOS, Linux system or WSL2 with both installed, you can alias the Docker command with Podman in your './.bashrc' or './.zhrc' depending on which shell environment you are using. This can be particulary helpful if you use 'Make' scripts, in your workflow that reference docker and would 
like them to use Podman. 

For further instructions on how to install Podman on another OS please visit the website [podman.io](https://podman.io/getting-started/installation).

## Algorithm of the week

In the last digest, we looked at the RSA method for sharing secrets. This week we are looking at key exchange with the Diffie-Hellman algorithm, 
created by [Whitfield-Diffie](https://en.wikipedia.org/wiki/Whitfield_Diffie) and [Martin Hellman](https://en.wikipedia.org/wiki/Martin_Hellman). I recently attended 
a talk given by Professor Hellman, where he shared the history of the algorithm and his experience as a cryptologist. The talk left me feeling inspired.

The Diffie-Hellman algorithm is another way to create a shared secret key. The algorithm works by two parties first agreeing to a large prime number $$p$$ 
and a generator number $$g$$. The generator is an element of $$\mathbb{Z}^{*}_{p}$$ a large order cyclic subgroup of $$\mathbb{Z}$$ so that, $$g\in\mathbb{Z}^{*}_{p}$$. 

Alice and Bob use the algorithm below to generate public keys. The private keys are represented by $$x_{alice}$$ and $$x_{bob}$$ and the public keys 
$$Y_{bob}$$ and $$Y_{alice}$$. The shared secret key is $$K$$. Bobs public key is found by:

\begin{align}
	Y_{bob}=g^{x_{bob}} \text{ mod } p \label{eq: Diffie-Hellman Public Key (Bob)}
\end{align}

Alice performs a similar calculation to derive her public key:

\begin{align}
	Y_{alice}=g^{x_{alice}} \text{ mod } p 
\end{align}

Now Bob can calculate the shared secret key from Alice's public key and his private key: 

\begin{align}
	K=(Y_{alice})^{x_{bob}} \text{ mod } p
\end{align} 

Alice can do the same: 

\begin{align}
	K=(Y_{bob})^{x_{alice}} \text{ mod } p
\end{align}

Why the algorithm works, can be shown using the equalities revealing $$K$$ in both equations for deriving the shared key.

\begin{align}
	\text{K by Bob} = (Y_{alice})^{x_{bob}} \text{ mod } p  
\end{align}

\begin{align}	
	= (g^{x_{alice}} \text{ mod } p )^{x_{bob}} \text{ mod } p
\end{align}

\begin{align}	
	= (g^{x_{alice}})^{x_{bob}} \text{ mod } p 
\end{align}

\begin{align}	
	= g^{x_{alice}{x_{bob}}} \text{ mod } p 
\end{align}
	
\begin{align}
	= (g^{x_{bob}})^{x_{alice}} \text{ mod } p 
\end{align}
	
\begin{align}
	= (g^{x_{bob}} \text{ mod } p )^{x_{alice}} \text{ mod } p 
\end{align}

\begin{align}
	= (Y_{bob})^{x_{alice}} \text{ mod } p = \text{K by Bob}
\end{align}

An illustrative example using simple numbers is given below:

1. First a private key is generated for each participant
	
	\begin{align}
		x_{alice}= 7, x_{bob} = 9 
	\end{align}	

2. A $$g$$ value and $$p$$ prime number are generated

	\begin{align}
		g = 5, p=97 
	\end{align}

3. The public key for both Alice and Bob can be calculated

	\begin{align}
		Y_{bob}=5^{9} \text{ mod } 97
	\end{align}
	
	\begin{align}
		Y_{alice}=5^{7} \text{ mod } 97
	\end{align}

4. the shared secret key can then be calculated by both Alice and Bob.
		
	\begin{align}
		K_{bob}=(Y_{alice})^{x_{bob}} \text{ mod } p
	\end{align}

	\begin{align}
		K_{alice}=(Y_{bob})^{x_{alice}} \text{ mod } p
	\end{align}	

### Important properties of Diffie-Hellman

- Having both $$Y_{bob}$$ and $$Y_{alice}$$ does not mean an attacker can figure out $$K$$
- Both parties can create the same shared key $$K$$ without ever having to share the actual key

Diffie-Hellman is susceptible to a man in the middle attack, where an attacker hijacks the session by intercepting both 
participants public keys and forwards an alternative. Both participants will not have the ability to check the authenticity of the keys they
received.



## Books Recommendations

| Title  | Author | ISBN |
|:-------|:-------|:-----|
| Podman for Devops| Alessandro Arrichiello and Gianni Salinetti | 978-1803248233 |
|Unit Testing:Principles, Practices and Patterns | Vladimir Khorikov | 978-1617296277 |
