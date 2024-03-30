# xurls

[![Go Reference](https://pkg.go.dev/badge/mvdan.cc/xurls/v2.svg)](https://pkg.go.dev/mvdan.cc/xurls/v2)

Extract urls from text using regular expressions. Requires Go 1.21 or later.

```go
import "mvdan.cc/xurls/v2"

func main() {
	rxRelaxed := xurls.Relaxed()
	rxRelaxed.FindString("Do gophers live in golang.org?")  // "golang.org"
	rxRelaxed.FindString("This string does not have a URL") // ""

	rxStrict := xurls.Strict()
	rxStrict.FindAllString("must have scheme: http://foo.com/.", -1) // []string{"http://foo.com/"}
	rxStrict.FindAllString("no scheme, no match: foo.com", -1)       // []string{}
}
```

Since API is centered around [regexp.Regexp](https://golang.org/pkg/regexp/#Regexp),
many other methods are available, such as finding the [byte indexes](https://golang.org/pkg/regexp/#Regexp.FindAllIndex)
for all matches.

The regular expressions are compiled when the API is first called.
Any subsequent calls will use the same regular expression pointers.

#### cmd/xurls

To install the tool globally:

	go install mvdan.cc/xurls/v2/cmd/xurls@latest

```shell
$ echo "Do gophers live in http://golang.org?" | xurls
http://golang.org
```
