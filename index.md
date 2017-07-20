---
layout: default
title: "Introduction to Kweb"
---

1. TOC
{:toc}

#### What is Kweb?

Kweb is a library for building single-page web applications in the [Kotlin](http://kotlinlang.org/)
programming language.  You can think of it as a powerful Kotlin DSL that allows you to remote-control
web browsers to a web server.

Even though your code runs on the server, Kweb allows you to interact to the browser DOM directly, for example here 
we create a `<p>` element and set its text:

```kotlin
doc.body.p().text("this is an example HTML paragraph")
```

You can also interact to JavaScript directly, although you should rarely need to do this:

```kotlin
doc.body.execute("console.log((new Date()).getDay());")
```

You can even query JavaScript and do something to the result:

```kotlin
val day = doc.body.evaluate("$('#day').text()")
database.update(BOOK).set(BOOK.DAY, day).execute()
```

Kweb has plugins for JavaScript libraries like [JQuery](https://jquery.com/) and 
[others](https://github.com/kwebio/core/tree/master/src/main/kotlin/io/kweb/plugins).  It's also 
surprisingly easy to build your own plugins for other JavaScript libraries, or extend those Kweb already
supports.

![status experimental](https://img.shields.io/badge/status-experimental-orange.svg) 
Kweb is currently **experimental**, please play with it, give us feedback, join our development effort, but remember that it is still a few months away (June 2017) from being suitable for non-experimental use.

#### Features
* Build websites in Kotlin
* Makes the barrier between web-browser and web-server largely invisible to the programmer
* Seamlessly integrates with powerful JavaScript libraries like JQuery, Semantic-UI, and others
* Update your web browser instantly in response to code changes
* Bind DOM elements in the browser directly to persistent state on the server and have them update automatically, through the [observer](https://en.wikipedia.org/wiki/Observer_pattern) and [data mapper](https://en.m.wikipedia.org/wiki/Data_mapper_pattern) patterns, and following the [single source of truth](https://en.wikipedia.org/wiki/Single_source_of_truth) principle)
* Easy to add to an existing project, Kweb is just a library, it doesn't seek to tell you how your project should
  be organized

#### How does it work?
Kweb keeps all of the logic server-side, and uses efficient websockets to communicate to web 
browsers. We also take advantage of Kotlin's powerful new coroutines mechanism to efficiently handle
asynchronicity, largly invisibly to the programmer.

#### What does it look like?

Here we create a simple "todo" list app:

```kotlin
fun main(args: Array<String>) {
    Kweb(8091, debug = true) {
        doc.body.new {
            h1().text("Simple Kweb demo - a to-do list")
            p().text("Edit the text box below and click the button to add the item.  Click an item to remove it.")

            val ul = ul().new {
                for (text in listOf("one", "two", "three")) {
                    newListItem(text)
                }
            }

            val inputElement = input(type = InputType.text, size = 20)
            button().apply {
                text("Add Item")
                on.click {
                    future {
                        val newItemText = inputElement.getValue().await()
                        ul.new().newListItem(newItemText)
                        inputElement.setValue("")
                    }
                }
            }
        }
    }
}

fun ElementCreator<ULElement>.newListItem(text: String) {
    li().apply {
        text(text)
        on.click {
            delete()
        }
    }
}
```
**Next: [Setting Up]({{ site.baseurl }}{% post_url 2017-03-03-getting-started %}) >>>>**
