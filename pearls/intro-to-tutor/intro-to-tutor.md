# M13 Samples

This document illustrates some of the markup and features of M13.

## Markdown

Documents are formatted using [Kramdown](http://kramdown.gettalong.org/),
so wander over there for details of its markup.

In addition, we have our own extensions.

### Inline styles

...such as _italic_, **bold**, and `code`.

### Unnumbered Lists

* unnumbered lists

* such as this

  * that can be nested

    and that can contain nested content such as paragraphs
    and code

### Numbered Lists

1. Numbered lists
1. That can also contain
   1. nested content
   2. like this
1. And that number themselves automatically.

(Note that lists are spaced if the Markdown is spaced.)

### Blockquotes

> It is rare to find learned men who are clean, do not stink and have
> a sense of humour. _(said about Leibnitz)_

### Popup Footnotes

When you create a Kramdown footnote[^fn-footnote] we convert it into a
popup window, triggered by a little info icon.

[^fn-footnote]:
    You use the syntax `[^fn-some-name]` to reference the footnote.
    Then, as a separate block element, use `[^fn-footnote]: ...` to
    define the content.

### Tables

Simple tables can be constructed using the Kramdown vertical-bar
syntax.

| A simple | table |
| with multiple | lines|
{: #first-table}

and more complex:

| First column | Middle column | Last Column |
|:--------|:-------:|--------:|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|----
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|=====
| Footer 1   | Footer 2   | Footer 3

with inner rules:

| First column | Middle column | Last Column |
|:--------|:-------:|--------:|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|----
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|=====
| Footer 1   | Footer 2   | Footer 3
{: .inner-rules}

### Code

Code is included between lines containing `~~~`. Put the programming
language name after the leading `~~~` to turn on syntax highlighting.

~~~~
~~~ ruby
def fred
  puts "hello" # cheery
end
~~~
~~~~

Produces:

~~~ ruby
def fred
  puts "hello" # cheery
end
~~~

### Links

* Named external links: the [PragProg site](https://pragprog.com)
* Internal links to [other sections](#numbered-lists)

Section headings automatically have id attributes set from the title.
You can also set the id manually for any other element using a block
attribute, so [this](#first-table) links to the first table.


# M13 Extensions

M13 adds a number of extensions to Markdown (and you can even add your
own).

All extensions work at the block level. They start with tags that look
like `{::«name» «params»…}` and end with
`{:/name}`. (You can omit the name part of the closing tag,
but please don't.)

## TLDR—Multi-level Documents

{::tldr}
Sometimes readers want just an overview. Sometimes they want the full
scoop.
The `{::tldr}` directive lets
you structure your documents with summaries and details.
Click on the `+` to see the details.

{++}
~~~ plain
The markup looks like this:
{::tldr}
content for the summary
(can be any content apart from tldr's)
{--} or {++}
content for the detail.

Again, can be any content
{:/tldr}
~~~

If you use `{--}` to separate the summary and the detail, then the
detail replaces the summary when expanded. If you use `{++}`, the
detail is appended to the summary.

Click on the `–` to hide the details.

{:/tldr}

## Terminal Session Playback

Use `m13/tools/recorder` to record terminal sessions, and
`m13/tools/edit_session` to edit the recorded session. Add the line
type `start` to indicate where in the session the recording should
start. Add popups if needed. Play the session back in your
document using `{::playback «filename» /}`.

{::playback example_recording/}

## Quizzes

Help your readers cement concepts. We support three types:

{::quiz "Multiple Choice"}

We've seen the word-signature transformation:

~~~ elixir
word |> split_into_letters |> sort |> join
~~~

How would you express this in a "conventional" language?

{::multiple-choice}
{::wrong "`word(split_into_letters(sort(join)))`"}
It would be nice if conventional languages let you write code as
if it were a sentence expressing your intent, but unfortunately they don't.
You have to write things backwards.
{:/wrong}

{::correct "`join(sort(split_into_letters(word)))`"}
You're right! But look what what we had to write. It's backwards. The
original transformation lays things out left-to-right. Our nested
method calls read right-to-left, inside to out.
{:/correct}
{:/multiple-choice}
{:/quiz}


{::quiz "Multiple Answer"}

Which of the following are prime numbers?

{::multiple-answer}
{::wrong 0}
Zero isn't prime, because any number times 0 is 0. Also, primes are
defined to be numbers greater than 1.
{:/wrong}

{::wrong 1}
Prime numbers are (by definition) greater than 1.
{:/wrong}

{::correct 2 "This one may surprise you!"}
Two is the only even prime number. Its only factors are 1 and 2.
{:/correct}

{::correct 3}
Three is prime—it's 1 &times; 3.
{:/correct}

{::wrong 4 "Hint: it isn't"}
Four is both 1 &times; 4 and 2 &times; 2.
{:/wrong}

{:/multiple-answer}
{:/quiz}


{::quiz "Fill in the Blanks"}

{::fill-in-the-blanks}
There are {::placeholder width="3" should-be="50|fifty"/}
stars on the US flag.
{:/fill-in-the-blanks}
{:/quiz}


## Dynamic Diagrams (Dynagram)

{::dynagram height=150}
% N = 4
% COLORS  = %w{ black #d40000 #aa0000 maroon #550000 #2a0000 red  }
% WOOD    = "fill: #c60 stroke_width: 0 stroke: red "
% TOWER   = "box 7 65 #{WOOD} with .s "
% MARGIN  = "box 9 65 fill: white stroke_width: 0 stroke: green with .s "

$title "Towers of Hanoi" font: "20pt sans-serif" fill: #797 with .n at stage.n

$move  "" font: "15pt sans-serif" fill: #aca with .n at title.s

group with .s stage.s {

    $base-a  box 80 8 <WOOD>
             hgap 20
    $base-b  box 80 8 <WOOD>
             hgap 20
    $base-c  box 80 8 <WOOD>

%   last = "base-a"
%   N.downto(1) do |n|
%       w =  16*n
%       col = COLORS[n]

        $disk<n> group with .s at <last>.n {
            $ring<n> box <w> 10 fill: <col> rounding: 4
                     vgap 2 with .n at ring<n>.s
        }

%       last = "disk#{n}"
%   end

             <MARGIN> at base-a.n
    $tower-a <TOWER>  at base-a.n
             <MARGIN> at base-b.n
    $tower-b <TOWER>  at base-b.n
             <MARGIN> at base-c.n
    $tower-c <TOWER>  at base-c.n


}

wait 2

<%=
@result = []
@state = {
       "a" => [ "base-a", "disk4", "disk3", "disk2", "disk1" ],
       "b" => [ "base-b" ],
       "c" => [ "base-c" ]
}

@move_no = 0

def show_move(n, from, to)
    @move_no += 1
    factor = 1.0 / Math.sqrt(Math.sqrt(@move_no))
    @result << %{set move.text "Move #{@move_no}" take: #{1.5*factor}}
    disk = @state[from].pop
    @result << "move disk#{n}.s to tower-#{from}.n take: #{0.7*factor} sync: true"
    @result << "move disk#{n}.s to tower-#{to}.n   take: #{1.5*factor} sync: true"
    @result << "move disk#{n}.s to #{@state[to].last}.n take: #{0.4*factor} sync: true"
    @state[to].push disk
end

def hanoi(n,a,b,c)
  result = []
  if n > 0
    hanoi(n-1, a, c, b)
    show_move(n, a, c)
    hanoi(n-1, b, a, c)
  end
end

hanoi(N, "a", "b", "c")

@result.join("\n")
%>

set move.text "Done"
{:/dynagram}

# Conditional Content

The `Necklace` file can define a set of options for your document.  These
options can control what the reader sees. For example, you may choose  to show
different command line sessions or installation instructions depending on the
operating system they use, or you might want to omit some of the background content for
more advanced readers.

The options section looks like this:

~~~ yaml
parameters:

  level     (Your level in this topic):
    - tyro  (Beginner)
    - pro   (Decent knowledge of programming)

  os          (The operating system you use):
    - osx     (OS X)
    - linux   (Linux/Unix)
    - windows (Windows)
~~~

This example defines two parameters, `level` and `os`. Each parameter has a number of available options (`tyro` and `pro` for `level`, and `osx/linus/windows` for `os`). The entries all consist of two parts: the name and a title. The name is used inside your document to identify the parameter and option, and the title (which is given between parentheses), is what the reader sees when they control parameter values.

Inside your document, you use these parameters using extension markup such as `{::if}` anf `{::choose}`. For example, you could have:

~~~ plaintext
{::if os.windows}

At this point in the installation, you will
need to restart your computer.

{:/if}
~~~

If the reader has selected the `windows` option for the `os` parameter, thqt paragraph will be displayed.

You can try this now. The following paragraphs will change if you select
different options for the operating system. Bring up the settings
box[^fn-settings] and try different options for the _Operating System You Use_
parameter.


[^fn-settings]: On a desktopm, click on _Settings_ in the sidebar. On mobile
                devices, use the gear icon in the topbar.

{::if os.windows}

### Finishing up the Windows Install

You are running on Windows, so you'll see something that looks like this:

![](images/windows.png)

{:/if}

{::if os.linux}

### Finishing up the Linux Install

On Linux, a typical desktop looks like this:

![](images/linux.png)

{:/if}

{::if os.osx}

### Finishing up on OS X

The OS X desktop will vary depending on the version you have installed,
but it will typically look something like this:

![](images/osx.jpg)

{:/if}
