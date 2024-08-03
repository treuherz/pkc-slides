---
theme: seriph
background: images/voynich126.jpg
title: Welcome to Slidev
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Public Key Cryptography

_A quick introduction, by Eli_

<!--
- Thank for coming
  - I've been threatening to do this talk for longer...
  - Writing is difficult and I'm quite lazy
  - Your patience is appreicated

- Set expectations
  - Tried not to assume much background, but  unavoidably technical.
  - Tried to avoid maths
  - Very initialism-heavy, tried to tamp down
  - Start below knowledge already have,
  - Hopefully by end risen above and we'll all have learnt something

- If baffling or wrong, jump in
  - Otherwise questions at end
-->

---
layout: image-right
image: images/voynich176.jpg
---

<div class="
  h-full
  flex
  flex-col
  flex-justify-center
  text-size-2xl
">
<v-clicks>

**Basics**

**SSH** <small>and key exchange</small>

**HTTPS** <small>and certificates</small>

</v-clicks>
</div>

---
layout: full
transition: slide-left
---

<p>
<b>Encryption:</b> Using an algorithm to combine some data with a key so it can only be read by an
intended recipient
</p>

<p v-click>
<b>Symmetric Encryption:</b> Using the same key to encrypt and decrypt data
</p>

<div class="eqn">
<span v-click>My Secret Data &#8727; <Key hue="150">K</Key></span> <span v-click>&#8658; <Encrypt key-id="K" hue="160">My Secret Data</Encrypt></span>
</div>

<div class="eqn">
<span v-click><Encrypt key-id="K" hue="160">My Secret Data</Encrypt></span> <span v-click>&#8727; <Key hue="160">K</Key> &#8658; My Secret Data</span>
</div>

<p v-click>
Chicken-and-Egg problem: You already need the key, <Key hue="150">K</Key>, to send or receive
anything
</p>


---
layout: full
transition: slide-left
---


<p>
<b>Asymmetric Encryption:</b> Algorithms which use one key for encryption, and another key for decryption.
</p>

<div v-click class="eqn">
  <Key hue="295">a</Key> and <Key hue="295">A</Key>
</div>

<div v-click class="eqn">
My Secret Data &#8727; <Key hue="295">A</Key> &#8658; <Encrypt key-id="A" hue="295">My Secret Data</Encrypt>
</div>

<div v-click class="eqn">
<Encrypt key-id="A" hue="295">My Secret Data</Encrypt> &#8727; <Key hue="295">a</Key> &#8658; My Secret Data
</div>

<p>
<span v-click>We can publish one of these keys, and keep the other private.</span>
<span v-click> Now we can send and receive encrypted data without sending a secret key.</span>
</p>

<!--
Asymmetric encryption is what we're focusing on today. The idea is different keys
[click] Let's call this pair of keys little a and big a
[click] You encrypt with one...
[click] But need to use the other to decrypt. The same would work in reverse

I don't want to go into the details of the maths today. All you need to know
is some very clever people developed these systems using the properties of certain
mathematical operations.

When people say prime numbers are important for cryptography, they mean this.

Rivest, Shamir and Adleman invented the first system that could do this in the '70s,
and it relies on prime numbers.

These days we also have systems that use operations on functions called Elliptic Curves as well.

[click] This lets us do something very clever.
[click] This is going to solve our chicken-and-egg problem.

Let's go through this in detail.

-->

---
layout: chat
transition: slide-left
---

<AliceThinks v-click=1>generates key-pair <AliceKey>(a, A)</AliceKey>.
  She keeps <AliceKey>a</AliceKey> private and publishes <AliceKey>A</AliceKey>
</AliceThinks>
<BobThinks v-click=2>generates key-pair <BobKey>(b, B)</BobKey>.
  He keeps <BobKey>b</BobKey> private and publishes <BobKey>B</BobKey>
</BobThinks>
<AliceThinks v-click=3>wants to send Bob a message only he can read</AliceThinks>
<AliceThinks v-click="[4, 5]">computes <em>&ldquo;made you look&rdquo; &#8727; <BobKey>B</BobKey> &#8658; <BobEncrypts key-id="B">made you look</BobEncrypts></em></AliceThinks>
<AliceThinks v-click="5">computes <em>&ldquo;made you look&rdquo; &#8727; <BobKey>B</BobKey> &#8658; <BobEncrypts key-id="B"><Censored>made you look</Censored></BobEncrypts></em></AliceThinks>
<Alice v-click=6 tag="To: bob@bob.com"><BobEncrypts key-id="B"><Censored>made you look</Censored></BobEncrypts></Alice>
<BobThinks v-click=7>computes <em><BobEncrypts key-id="B"><Censored>made you look</Censored></BobEncrypts> &#8727; <BobKey>b</BobKey> &#8658; &ldquo;made you look&rdquo; </em></BobThinks>
<Bob v-click=8 tag="To: alice@alice.net">😑 😑 😑</Bob>

---
layout: full
transition: slide-left
---


<p>
<b>Signing</b> is a special usage of this where you encrypt something with your own private key.
</p>

<div v-click class="eqn">
Alice is very clever &#8727; <AliceKey>a</AliceKey> &#8658; <AliceEncrypts key-id="a">Alice is very clever</AliceEncrypts>
</div>

<p v-click>
Anyone can decrypt this with Alice&rsquo;s public key <AliceKey>A</AliceKey> and confirm Alice wrote it.
</p>

<p v-click>
A <b>signature</b>  proves authorship of its contents, or ownership of a key
</p>

---
layout: full
transition: slide-left
---

<p>
<b>Hashing:</b> running a <em>deterministic</em>, <em>irreversible</em> computation to transform data to
  into a <em>fixed-size</em> output, a.k.a. a <b>hash</b> or <b>checksum</b>.
</p>

<div v-click class="eqn" >
hash(&ldquo;My cool input&rdquo;) &#8658; &ldquo;6cdc01e200329e91...&rdquo;
</div>

<ul style="font-size: 24pt">
<li v-click>Checking integrity of files</li>
<li v-click>Storing passwords safely</li>
<li v-click>Posting plot-twist predictions to Twitter</li>
</ul>

---
layout: image-right
image: images/voynich174.jpg
---

<p>
<em>We can now...</em>
</p>

<p v-click>
send a message only readable by an intended recipient
</p>

<p v-click>
prove a message was encrypted by someone
</p>

<p v-click>
prove posession of some data without sending it
</p>

---
layout: image-left
image: images/voynich111.jpg
---

## SSH Handshake

<p> Setting up an encrypted channel without sharing a key beforehand </p>

---
layout: chat
transition: slide-left
---

<AliceThinks v-click="[1, 6]">dials Bob&rsquo;s server on port 22</AliceThinks>
<Alice v-click="[1, 6]" tag="TCP SYN">Hi, how are you?</Alice>
<Bob v-click="[2, 6]" tag="TCP SYN, ACK">Hi, I'm ok, how are you?</Bob>
<Alice v-click="[3, 6]" tag="TCP ACK">I'm ok too </Alice>

<Alice v-click="4" tag="SSH identification string">I want to run SSH</Alice>
<Bob v-click="5" tag="SSH identification string">Me too</Bob>
<Alice v-click="6" tag="SSH_MSG_KEXINIT">These are all the algorithms I support...</Alice>
<Bob v-click="7" tag="SSH_MSG_KEXINIT">These are all the algorithms I support...</Bob>

<!--
[click] I'm going to paraphrase message content
[click] Ordinary TCP 3-way handshake.
[click]
[click] Now the SSH software on both sides announces itself
[click]
[click] Start the key exchange process by telling the other system what algorithms we support
[click] You might think you'd send your SSH key, but you'd be wrong
-->

---
layout: full
transition: slide-right
---

## Key exchange

<v-clicks>

**Speed:** Asymmetric encryption is hundreds of times slower than symmetric

**Forward Secrecy:** If your key is compromised, so is everything you've ever done with it

We need a way to make **symmetric**, **short-lived** keys

The algorithm we'll use is called **Diffie-Hellman Key Exchange**

</v-clicks>

<!--
Good reasons not to use our usual public/private key-pairs
[click] Speed
[click] If those keys leak, they compromise every past use of them
-->

---
layout: chat
transition: slide-up
---

<AliceThinks v-click="[1, 6]">generates a key-pair <AliceKey>(p, P)</AliceKey></AliceThinks>
<Alice v-click="[2, 6]" tag="SSH_MSG_KEX_ECDH_INIT">Here's my ephemeral public key, <AliceKey>P</AliceKey></Alice>

<BobThinks v-click="[3, 6]">generates a key-pair <BobKey>(q, Q)</BobKey></BobThinks>
<BobThinks v-click="4">combines <AliceKey>P</AliceKey> and <BobKey>q</BobKey> to produce a shared key, <Key hue="150">K</Key></BobThinks>
<Bob v-click="[5, 10]" tag="SSH_MSG_KEX_ECDH_REPLY">Here's my static public key <BobKey>B</BobKey>, my ephemeral public key <BobKey>Q</BobKey>, and <em>hash(<Key hue="150">K</Key>)</em></Bob>

<AliceThinks v-click="[7, 10]">checks <BobKey>B</BobKey> matches her records</AliceThinks>
<AliceThinks v-click="8">combines <AliceKey>p</AliceKey> and <BobKey>Q</BobKey> to produce the same shared key, <Key hue="150">K</Key></AliceThinks>
<AliceThinks v-click="9">calculates <em>hash(<Key hue="150">K</Key>)</em> and confirms it matches what Bob sent</AliceThinks>

<hr v-click="10" class="my-5"/>

<p v-click="11"><Key hue="150">K</Key> is a short-lived and symmetric key</p>
<p v-click="12">Alice and Bob created it co-operatively <em>and</em> independently</p>
<p v-click="13">They got the same result without transmitting private material</p>

<!--
Back to Alice and Bob.
[click] Going to abstract over the maths again
[click][click][click][click][click][click][click] That was kind of weird, so let's linger here

We've done maths on two different pieces of information and got the same result. The properties here are important.

[click] This is what we wanted by doing this at all
[click] They both had to participate to get this result, and can check each other's work
[click] They sent a hash, but not K itself, so everything private is private.

We've put together a secure channel with these useful properties. That's Diffie Hellman key exchange.

-->

---
layout: chat
transition: slide-left
---

<Alice v-click="1" tag="SSH_MSG_USERAUTH_REQUEST">
  <Encrypt key-id="K" :hue="150">Here's my password</Encrypt>
</Alice>
<BobThinks v-click="2">checks the password against his records</BobThinks>
<Bob v-click="2" tag="SSH_MSG_USERAUTH_SUCCESS">
  <Encrypt key-id="K" :hue="150">Looks good, come in</Encrypt>
</Bob>

<hr class="my-3" v-click="2"/>

<Alice v-click="3" tag="SSH_MSG_USERAUTH_REQUEST">
  <Encrypt key-id="K" :hue="150">Here's <AliceKey>A</AliceKey> and <AliceEncrypts key-id="a"><em>hash(<Key hue="150">K</Key>)</em></AliceEncrypts></Encrypt>
</Alice>
<BobThinks v-click="4">checks <AliceKey>A</AliceKey> against his records and uses it to confirm the signed hash</BobThinks>
<Bob v-click="5" tag="SSH_MSG_USERAUTH_SUCCESS">
  <Encrypt key-id="K" :hue="150">Looks good, come in</Encrypt>
</Bob>

<!--
We encrypt every message now with K. Last step is for Alice to prove her identity

[click] We've got a secure channel, so we can send passwords safely
[click]  This talk is about keys, passwords are boring

[click] Alice sends key and sig
[click] Bob checks A against `authorized_keys`
[click] Bob confirms sig

-->

---
layout: image-right
image: images/voynich177.jpg
---

## SSH Handshake

<v-clicks>

Alice verified the server is really Bob

Bob verified the client is really Alice

They've got an encrypted channel for the session, so nobody can snoop

</v-clicks>

<!--
We've used all our building blocks to do something actually, tangibly useful
-->

---
layout: image-left
image: images/voynich156.jpg
---

## TLS Handshake

<v-clicks>

Diffie-Hellman still works for setting up an encrypted channel

Proving server identity is harder

</v-clicks>

<!--
TLS is the protocol that secures HTTPS exchanges

There's a handshake before the HTTP request in the same way as SSH

More difficult is figuring out if you're talking to who you think you're talking to.
-->

---
layout: chat
transition: slide-left
---

<AliceThinks v-click="[0, 1]">dials Bob&rsquo;s server on port 443</AliceThinks>
<Alice v-click="[0, 1]" tag="TCP SYN">Hi, how are you?</Alice>
<Bob v-click="[0, 1]" tag="TCP SYN, ACK">Hi, I'm ok, how are you?</Bob>
<Alice v-click="[0, 1]" tag="TCP ACK">I'm ok too </Alice>

<AliceThinks v-click=1>generates a key-pair <AliceKey>(p, P)</AliceKey></AliceThinks>
<Alice v-click=1 tag="Client Hello">Here's <AliceKey>P</AliceKey></Alice>

<BobThinks v-click=2>generates a key-pair <BobKey>(q, Q)</BobKey></BobThinks>
<Bob v-click=2 tag="Server Hello">Here's <BobKey>Q</BobKey></Bob>
<BobThinks v-click=3>combines <AliceKey>P</AliceKey> and <BobKey>q</BobKey> to produce a shared key, <Key hue="150">K</Key></BobThinks>
<AliceThinks v-click=3>combines <AliceKey>p</AliceKey> and <BobKey>Q</BobKey> to produce the same shared key, <Key hue="150">K</Key></AliceThinks>

<Bob v-click=4 tag="Server Certificate">
  <Encrypt key-id="K" :hue="150">Here's my certificate, <CarlosEncrypts key-id="c"><BobKey>B</BobKey>:&nbsp;bob.com</CarlosEncrypts></Encrypt>
</Bob>

<!--
This starts the same way, with a TCP 3-way handshake

[click] And continues the same way with DHE
[click]
[click]

[click]
In SSH, Bob just sent a public key. What happens when you get a public key you don't recognise?
Not good enough for web

Instead Bob sent key signed by C. Who's C?

-->

---
layout: chat
transition: slide-up
---

<p v-click>
A <b>certificate</b> is a signed file connecting an identity and a public key.
</p>

<p v-after>
It's signed by a <b>certificate authority</b> (CA).
</p>

<CarlosThinks v-click >
  runs a CA, so he generates a key-pair <Key hue="0">(c, C)</Key>.
</CarlosThinks>

<CarlosThinks v-click>
  self-signs a <b>root certificate</b>: <em><CarlosEncrypts key-id="c"><Key hue="0">C</Key>:&nbsp;Carlos&rsquo; CA</CarlosEncrypts></em>
</CarlosThinks>

<p v-click>
These root certificates and their public keys are distributed with operating systems and browsers.
</p>


---
layout: chat
transition: slide-right
---

<Bob v-click="[1, 4]">I'd like to set up HTTPS on bob.com. Here's my public key <BobKey>B</BobKey> and a signature: <BobEncrypts key-id="b">bob.com</BobEncrypts>.</Bob>

<Carlos v-click=2>Here's a token, &ldquo;b0b5m311s&rdquo;. Prove you own bob.com.</Carlos>

<hr v-click=3 class="my-3">

<BobThinks v-click=3>puts the token on his website</BobThinks>
<Bob  v-click=3 tag="bob.com/.well-known/acme-challenge">b0b5m311s</Bob>

<hr v-click=4 class="my-3">

<BobThinks v-click=4>puts the token on his DNS host</BobThinks>
<Bob v-click=4 tag="TXT _acme-challenge.bob.com">b0b5m311s</Bob>

<Carlos v-click=5>Thanks, here's a certificate: <CarlosEncrypts key-id="c"><BobKey>B</BobKey>: bob.com</CarlosEncrypts></Carlos>

---
layout: chat
transition: slide-left
---

<Bob tag="Server Certificate">
  <Encrypt key-id="K" :hue="150">Here's my certificate, <CarlosEncrypts key-id="c"><BobKey>B</BobKey>:&nbsp;bob.com</CarlosEncrypts></Encrypt>
</Bob>

<AliceThinks v-click>checks her OS' root certs and finds <em><CarlosEncrypts key-id="c"><Key hue="0">C</Key>:&nbsp;Carlos&rsquo; CA</CarlosEncrypts></em></AliceThinks>
<AliceThinks v-click>she uses <Key hue="0">C</Key> to verify the signature on Bob&rsquo;s certificate</AliceThinks>

<Alice v-click tag="HTTP GET /"><Encrypt key-id="K" hue="0">Looks good, now please send me this page...</Encrypt></Alice>


---
layout: image-right
image: images/voynich156b.jpg
---

## TLS Handshake

<v-clicks>

We rely on CAs and distributors to vouch for server identity

You can run this infrastructure privately but it's a pain

</v-clicks>

---
layout: image-left
image: images/voynich124.jpg
---

## Summary

<v-clicks>

A lot of very smart people have let us rely on maths for trust and secrecy.

Do roll your own crypto, but don't deploy it to prod.

</v-clicks>

---
layout: end
---

# Questions?
