# Slides for public-key cryptography talk

To start the slide show:

- `pnpm install`
- `pnpm run dev`
- visit <http://localhost:3030>

Built with [Slidev](https://sli.dev/).

## Reading list

- Various SSH RFCs - they're easier to understand than you'd think
  - [RFC 4251](https://datatracker.ietf.org/doc/html/rfc4251): SSH Protocol Architecture
  - [RFC 4253](https://datatracker.ietf.org/doc/html/rfc4253): SSH Transport Layer Protocol, covering the packet format and initial handshake.
  - [RFC 4252](https://datatracker.ietf.org/doc/html/rfc4252): SSH Authentication Protocol, covering authenticating the client
  - [RFC 4254](https://datatracker.ietf.org/doc/html/rfc4254): SSH Connection Protocol, covering the remote terminal or whatever you're running
- [golang.org/x/crypto/ssh](https://pkg.go.dev/golang.org/x/crypto/ssh), the go SSH package. The code in here is again more readable than you might expect.
- [Understanding the SSH Encryption and Connection Process, by Justin Ellingwood](https://www.digitalocean.com/community/tutorials/understanding-the-ssh-encryption-and-connection-process). This was a helpful primer
- [Implementing a toy version of TLS 1.3, by Julia Evans](https://jvns.ca/blog/2022/03/23/a-toy-version-of-tls/). Julia writes fantastic blogs unpicking difficult concepts
- [The Illustrated TLS 1.3 Connection](https://tls13.xargs.org/). This shows every back and forth of a TLS 1.3 handshake. Fantastic website but the protocol is a bit of a nightmare.
- Books
  - [The Code Book, by Simon Singh](https://simonsingh.net/books/the-code-book/). Pop-sci, very readable.
  - [Applied Cryptography, by Bruce Schneier](https://www.schneier.com/books/applied-cryptography/). Massive textbook, probably a bit out of date these days but I read quite a bit of it long ago and it'd be rude to leave it out.
