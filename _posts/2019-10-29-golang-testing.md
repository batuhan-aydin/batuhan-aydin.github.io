---
layout: post
title:  "Golang Testing"
date:   2019-10-24 06:20:00 +0700
categories: ['go']
---

We are going to write testing only for hello world, to learn the basics for testing in go.

First we are creating hello.go file

{% highlight ruby %}
package main

// constants
const spanish = "Spanish"
const french = "French"
const turkish = "Turkish"
const englishHelloPrefix = "Hello, "
const spanishHelloPrefix = "Hola, "
const frenchHelloPrefix = "Bonjour, "
const turkishHelloPrefix = "Merhaba, "

// our function to test
func Hello(name, language string) {
    if name == "" {
        name = "World"
    }
    return greetingPrefix(language) + name
}

// helper function. notice it doesn't start with capital letter, because it is private
func greetingPrefix(language string) (prefix string) {

	switch language {
	case spanish:
		prefix = spanishHelloPrefix
	case french:
		prefix = frenchHelloPrefix
	case turkish:
		prefix = turkishHelloPrefix
	default:
		prefix = englishHelloPrefix
	}

	return
}

func main() {

}
{% endhighlight %}

Now testing part.
1- It should be name xxx_test.go. In this case we are naming hello_test.go
2- Testing function should start with 'Test'
3- It should take one argument, *testing.T. This argument will provide various functions for us to use

{% highlight ruby %}

package main

import "testing"

func TestHello(t *testing.T) {
    // helper function. notice we added t.Helper() so the program will know it is only helper, and the output will not be wrong(like which line we got the error)
	assertCorrectMessage := func(t *testing.T, got, want string) {
		t.Helper()
		if got != want {
			t.Errorf("got %q want %q", got, want)
		}
	}
    // first string is to describe the test, second testing function
	t.Run("saying hello to people", func(t *testing.T) {
		got := Hello("chris", "")
		want := "Hello, chris"
		assertCorrectMessage(t, got, want)
	})
    // always test every possibility
	t.Run("saying 'Hello, world' when empty string is given", func(t *testing.T) {
		got := Hello("", "")
		want := "Hello, World"
		assertCorrectMessage(t, got, want)
	})

	t.Run("in spanish", func(t *testing.T) {
		got := Hello("Elodie", "Spanish")
		want := "Hola, Elodie"
		assertCorrectMessage(t, got, want)
	})

	t.Run("in turkish", func(t *testing.T) {
		got := Hello("Batuhan", "Turkish")
		want := "Merhaba, Batuhan"
		assertCorrectMessage(t, got, want)
	})
}


{% endhighlight %}

Now you can write go test to terminal to see the results. You can write, break, then fix to understand more. 