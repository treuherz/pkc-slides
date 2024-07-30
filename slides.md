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
  - Tried not to assume much background, but  unavoidably technical
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

<style>
  :root {
    --uno: "text-size-2xl"
  }
</style>

<div class="
  h-full
  flex
  flex-col
  flex-justify-center
">
<v-clicks>

**Basics**

**SSH** <small>with an aside on key exchange</small>

**TLS** <small>with an aside on certificates</small>

</v-clicks>
</div>

---
layout: chat
transition: slide-left
---

<AliceThinks v-click="[0, 6]">dials Bob's server on port 22</AliceThinks>
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

<AliceThinks v-click="[1, 6]">generates a key-pair <em>(p, P)</em></AliceThinks>
<BobThinks v-click="[2, 6]">generates a key-pair <em>(q, Q)</em></BobThinks>
<Alice v-click="[3, 6]" tag="SSH_MSG_KEX_ECDH_INIT">Here's my public key, <em>P</em></Alice>

<BobThinks v-click="4">combines <em>P</em> and q to produce a shared key, <em>K</em></BobThinks>
<Bob v-click="[5, 9]" tag="SSH_MSG_KEX_ECDH_REPLY">Here's <em>B</em>, <em>Q</em> and <em>hash(K)</em></Bob>

<AliceThinks v-click="[7, 9]">checks <em>B</em> matches her records</AliceThinks>
<AliceThinks v-click="8">combines <em>p</em> and <em>Q</em> to produce the same shared key, <em>K</em></AliceThinks>

<hr v-click="9" class="my-3"/>

<p v-click="10"><em>K</em> is a short-lived and symmetric key</p>
<p v-click="11">Alice and Bob created it co-operatively <em>and</em> independently</p>
<p v-click="12">They got the same result without transmitting private material</p>

<!--
Back to Alice and Bob.
[click] Going to abstract over the maths again
[click][click][click][click][click][click][click] That was kind of weird, so let's linger here

We've done maths on two different pieces of information and got the same result. The properties here are important.

[click] This is what we wanted by doing this at all
[click] They both had to participate to get this result, and can check each other's work
[click] They sent a hash, but not K itself, so everything private is private

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
  <Encrypt key-id="K" :hue="150">Here's <em>A</em> and <AliceEncrypts key-id="a"><em>hash(K)</em></AliceEncrypts></Encrypt>
</Alice>
<BobThinks v-click="4">checks <em>A</em> against his records</BobThinks>
<BobThinks v-click="5">uses <em>A</em> to confirm the signed hash</BobThinks>
<Bob v-click="6" tag="SSH_MSG_USERAUTH_SUCCESS">
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
layout: image-left
image: images/voynich177.jpg
---

**That was an SSH handshake**

<v-clicks>

Alice verified the server has Bob's private key

Bob verified the client has Alice's private key

They've got an encrypted channel for the session

</v-clicks>
