# Gomail

This is an actively maintained fork of [Gomail][1] and includes fixes and
improvements for a number of outstanding issues. The current progress is
as follows:

 - [x] Support Go Module.
 - [ ] Filenames are properly encoded for non-ASCII characters.
 - [ ] Email addresses are properly encoded for non-ASCII characters.
 - [ ] Embedded files and attachments are tested for their existence.
 - [ ] An `io.Reader` can be supplied when embedding and attaching files.

See [Transitioning Existing Codebases][2] for more information on switching.

[1]: https://github.com/go-mail/mail/tree/v2
[2]: #transitioning-existing-codebases

## Introduction

Gomail is a simple and efficient package to send emails. It is well tested and
documented.

Gomail can only send emails using an SMTP server now. But the API is flexible and it
is easy to implement other methods for sending emails using a local Postfix, an
API, etc.

It requires Go 1.11 or newer, no external dependencies are used.

## Features

Gomail supports:
- Attachments
- Embedded images
- HTML and text templates
- Automatic encoding of special characters
- SSL and TLS
- Sending multiple emails with the same SMTP connection

## Documentation

https://godoc.org/github.com/imsingee/go-mail


## Download

Simple use `go get`

```
go get github.com/ImSingee/go-mail
```

## Examples

See the [examples in the documentation](http://godoc.org/github.com/imsingee/go-mail#example-package).


## FAQ

### x509: certificate signed by unknown authority

If you get this error it means the certificate used by the SMTP server is not
considered valid by the client running Gomail. As a quick workaround you can
bypass the verification of the server's certificate chain and host name by using
`SetTLSConfig`:

```go
package main

import (
	"crypto/tls"

	"github.com/ImSingee/gomail"
)

func main() {
	d := gomail.NewDialer("smtp.example.com", 587, "user", "123456")
	d.TLSConfig = &tls.Config{InsecureSkipVerify: true}

	// Send emails using d.
}
```

Note, however, that this is insecure and should not be used in production.

### Transitioning Existing Codebases

If you're already using the original Gomail, switching is as easy as updating
the import line to:

```
import "github.com/ImSingee/gomail"
```

## Contribute

Contributions are more than welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for
more info.


## Change log

See [CHANGELOG.md](CHANGELOG.md).


## License

[MIT](LICENSE)


## Support & Contact

You can ask any questions on the issue.
