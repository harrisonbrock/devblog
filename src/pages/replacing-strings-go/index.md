---
title: Replacing Parts of a String
date: 2018-11-11 20:00:00
featuredImage: './gostring.jpg'
---

Every developer needs to know how to work with strings in the language they are using. The Go libraries makes replacing parts of strings easy for a developer. I will show three solutions for replacing parts of a string in Go.

__Solution 1__

The simple way is to use the **[Replace](https://golang.org/pkg/strings/#Replace)** function from the **[strings](https://golang.org/pkg/strings/)** package. This function takes in four values:

1. **s**: This is the reference string.
1. **old**: This is the value in the string we want to change.
1. **new string**: This is the new string value.
1. **n**: This is the number of times to do the replacement. **If you use -1 it will replace all string values that are equal to the old value**

<!-- more-->
```go
package main

import (
	"strings"
	"fmt"
)

const refString = "Marry had a little duck duck duck"
func main() {

	// Use this for simple replacement
	// using -1 tell to replace all matches
	out := strings.Replace(refString, "duck", "Gopher", 2)

	fmt.Println(out)
}
```

This is the output:

```commandline
Marry had a little Gopher Gopher duck
```

If we change line 13 above to:

```go
out := strings.Replace(refString, "duck", "dog", -1)
```

This is the output:

```commandline
Marry had a little Gopher Gopher Gopher
```

__Solution 2__

When you have more than one string value to replace you should use the **[NewReplacer](https://golang.org/pkg/strings/#NewReplacer)** function from the **[strings](https://golang.org/pkg/strings/)** packages. This function
returns a **[new Replacer from a list of old, new string pairs](https://golang.org/src/strings/replace.go?s=676:720#L13)**. This method can be use to replace multiple string a once.

```go
package main

import (
	"strings"
	"fmt"
)

const refString = "Marry had a little duck duck"
func main() {
	
	replacer := strings.NewReplacer("Marry", "John", "duck", "Gopher")

	out := replacer.Replace(refString)

	fmt.Println(out)
}
```

This is the output:

```commandline
John had a little Gopher Gopher
```

__Solution 3__

The more sophisticated way of replaces substring is to use regular expression or regex. For this solution, we will use the **[MustCompile](https://golang.org/pkg/regexp/#MustCompile)** and **[ReplaceAllString](https://golang.org/pkg/regexp/#Regexp.ReplaceAllString)** from the **[regexp](https://golang.org/pkg/regexp/)** package.

1. **MustCompile**: Creates our regular expression. In this case, it’s a string that starts with d and is followed by any characters between a and z.
2. **ReplaceAllStrings**: This will replace substring that matches the regular expression the string Gopher 

```go
package main

import (
	"regexp"
	"fmt"
)

const refString = "Marry had a little duck duck"
func main() {

	regex := regexp.MustCompile("d[a-z]+")
	out := regex.ReplaceAllString(refString, "Gopher")
	fmt.Println(out)
}
```

This would output:

```commandline
Marry had a little Gropher Gopher
```