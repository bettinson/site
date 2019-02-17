---
layout: post
title: "Carrot Lang progress"
date:   2016-12-07 19:39:33 -0500
---

I think writing and teaching is a good way to cement knowledge about things I'm building, so I thought I would write about things I'm working on.

Recently, I've been hacking away on a language called Carrot. This is essentially a templating language that I'm
going to use for my Rails app [Imageup](http://104.131.50.247). Here is how I'm tackling the lexing. Part two on parsing will follow.

If you're not familiar with templating languages, the gist of it is to be able to turn this:


{% highlight html %}
<body>
  { { name="Matt" } }
  <p>Hi, This is {{ name }}'s website.</p>

  { { photos } }
  <img src={ { photo.path } }>
  { { photos } }
</body>

{% endhighlight %}

(note: the syntax isn't actually, `{ {`, it's without a space, which is the same as Jekyll's syntax)

into *this*:

{% highlight html %}
<body>
  <p>Hi, This is Matt's website.</p>

  <img src="photo1.jpg", alt="1", height="50", width="100">
  <img src="photo2.jpg", alt="2", height="50", width="70">
</body>
{% endhighlight %}


What this allows is for users to specify the layout of their personal photos page in a convenient and safe way. You can specify variables
with the `=` operator, obviously, and eventually you'll be able to use block syntax such as `{ { photos } }` to iterate through all
your photos.

If you have no idea how something like this would work, I'll try to explain. My way is definitely not the best way; this is simply a high level overview of how I tackled the problem.
Hopefully it will be useful to _somebody_.

So to first figure out what the `.html.crt` file is doing, we must *lex* the file. This means turning the file into a bunch of symbols
that hold two things: a value and the type of symbol. Heres a snippet that iterates through a single line:

{% highlight ruby %}

string.split('').select.each do |s|
    case s
    when /^[[:alpha:]]$/ # Is letters
        @current_word << s
    when '\''
        inQuotes ? inQuotes = false : inQuotes = true
        @current_word << s
    when ' '
        add_symbol(:word, :space, s)
{% endhighlight %}

This a very messy way of doing it, I think; I purposely set out on my own path to learn. The lexer goes through the file, appending regular
characters to `@current_word`, based on things such as if `inQuotes` is true (this means we're looking at a `:word` symbol), or if
`@current_word` is empty or not. After appending characters to `@current_word`, when I find a reserved
character, such as an assignment operator, I create a new symbol with `@current_word` and the word's type, and another symbol with the reserved
character. Heres an example of this:

{% highlight ruby %}
when '='
    add_symbol(:word, :equals, s)
{% endhighlight %}

{% highlight ruby %}
private
def self.add_symbol(previousToken, nextToken, s)
    @tokens << Token.new(@current_word, previousToken) unless @current_word == ""
    @current_word = ""
    @tokens << Token.new(s, nextToken)
end
{% endhighlight %}

This code handles the assignment operator. It creates a `:word` symbol and then creates an `:equals` symbol, each with the coresponding value and
type.

Lexing is pretty much a solved problem for Carrot lang at the moment. Parsing, on the other hand, is still in flux. I will
verbalize how I do parsing in another post. After exams probably. Then maybe one on how I integrated it into Imageup.
