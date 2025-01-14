---
date: '2025-01-14T11:50:54.000Z'
title: A History of Python's Error Messages
tagline: With Comments from a lead Python contributor
preview: >-
    Python's error messages have gone from frustrating and confusing, to clear, helpful and intuitive. Here's a history of how it improved.
image: >-
  https://images.unsplash.com/photo-1656188505561-19f1a1b6cda8?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1632&q=80
---

### The History of Python’s Error Messages

#### With comments from a leading Python contributor

It’s hard to ignore Python. It’s now far and away the most popular coding language, steadily surpassing classical languages such as Java and C++ in popularity.

[https://www.tiobe.com/tiobe-index/](https://www.tiobe.com/tiobe-index/)

I was not a programming prodigy. Python was my first the first coding language I dipped my toes in when I was 17. I tried to write a basic Python script in 3.6 and promptly gave up. 

Thanks to my schoolwork, I’ve been using Python a lot ever since. I’ve followed the Python updates throughout in my projects, school work, research, going from 3.8 to present day 3.13 and beyond.

Back then, everything was overwhelming. I distinctly remember learning about errors, exceptions and warnings. A ‘syntax error’ likely meant I had a typo, indentation error meant I didn’t properly use python’s indentation syntax, and index error meant I tried to access a value that wasn’t created within a list. But beyond that, there was no indication or help of where my errors were happening, unless I learned some complex debugging tools.

That being said, within that time, I python’s error messages have gone from frustrating and confusing, to **clear**, **helpful** and **intuitive**.

**And it’s not getting enough attention, nor enough credit.**

For example, see below error messages for the _exact same_ code below, for two different Python versions:

In Python 3.6:

and in Python 3.12: 

You see, maybe I wouldn’t have given up on programming all those years back if I started with Python 3.12 instead of 3.6.

#### The History of Python Error Messages, Through Version Change Logs

Suddenly appreciating the changes the Python development team has made throughout the years, I took it upon myself to dive into the archives of Python to learn all I could about the history of its errors, warnings, and messaging. 

Here’s what I found:

#### Pre Python 2.0

Python was the creation of Guido van Rossum’s. It was heavily based on the [ABC programming language](https://en.wikipedia.org/wiki/ABC_(programming_language)), created at his time at the [Centrum Wiskunde &amp; Informatica (CWI)](https://www.cwi.nl/en/). 

Version 1.0.0 was technically first released in 1994.

Indeed, in Python’s creators word from his [2009 blog post](https://python-history.blogspot.com/2009/01/pythons-design-philosophy.html): 

* “Errors should not be fatal. That is, user code should be able to recover from error conditions as long as the virtual machine is still functional.
* At the same time, errors should not pass silently (These last two items naturally led to the decision to use exceptions throughout the implementation.)
* A bug in the user’s Python code should not be allowed to lead to undefined behavior of the Python’s interpreter; a core dump is never the user’s fault.”

In python, errors and warnings are known under the umbrella term _exceptions._ As of python 3.13.0, there are 37 different errors types, with 11 warnings types. It has quite an intense [hierarchy](https://docs.python.org/3/library/exceptions.html#exception-hierarchy), as can be seen below.

Python Hierarchy of Exceptions for Python 2.7.18 (2020)

These are all objects that help inform user on potential bugs or incompatibilities within their code the might prevent them from achieving their wanted behavior.

This exception hierarchy has changed **a lot** since the birth of Python, as seen in the Python 2.7.18 example above.

#### 2.0

With this in mind, development of Python continued. Errors were made with Overflow Checking. When it came time to Python’s open-source 2.0 release (away from [CNRI](https://en.wikipedia.org/wiki/Corporation_for_National_Research_Initiatives)) in 2000. Two new subclasses were defined: the TabError and IndentationError, subsets of the previously stand-alone Syntax Error. With this, the basic hierarchy of eros were defined, making it so no error would ever pass undefined — there would always be a controllable exception for each Python error situation.

* **StandardError** (Base class for built-in exceptions that are not system-exiting):
* **ArithmeticError** (Base class for arithmetic exceptions):
* **OverflowError**: Raised when a numerical result exceeds the maximum limit for a numeric type.
* **ZeroDivisionError**: Raised when division or modulo by zero occurs.
* **FloatingPointError**: Raised when a floating point operation fails.
* **LookupError** (Base class for indexing errors)
* **IndexError**: Raised when a sequence subscript is out of range.
* **KeyError**: Raised when a dictionary key is not found.
* **EnvironmentError** (Base class for I/O related errors):
* **IOError**: Raised when an I/O operation (such as file opening) fails.
* **OSError**: Raised for OS-related errors, such as “file not found” or “access denied.”
* **EOFError**: Raised when the input() or raw\_input() functions hit an end-of-file condition.
* **ImportError**: Raised when an import statement fails to find the module definition.
* **MemoryError**: Raised when an operation runs out of memory.
* **NameError**: Raised when a local or global name is not found.
* **UnboundLocalError**: A subclass of NameError, raised when a local variable is referenced before assignment.
* **ReferenceError**: Raised when a weak reference is used to access an object that has been garbage collected.
* **RuntimeError**: Raised when an error is detected that doesn’t fall in any of the other categories.
* **NotImplementedError**: A subclass of RuntimeError. Raised when an abstract method is called that is not implemented.
* **SyntaxError**: Raised when the parser encounters a syntax error.
* **IndentationError** (Introduced in Python 2.0): A subclass of SyntaxError, raised when indentation is incorrect.
* **TabError** (Introduced in Python 2.0): A subclass of IndentationError, raised when tabs and spaces are mixed in indentation.
* **TypeError**: Raised when an operation or function is applied to an object of inappropriate type.
* **ValueError**: Raised when a function receives an argument of the correct type but an inappropriate value.
* **UnicodeError**: A subclass of ValueError. Raised when a Unicode-related encoding or decoding error occurs.
* **AttributeError**: Raised when an attribute reference or assignment fails.
* **SystemError**: Raised when the interpreter finds an internal error, but the situation is not critical enough to make it exit.
* **AssertionError**: Raised when an assert statement fails.
* **StopIteration**: Raised to signal the end of an iterator’s items (used to stop loops).

_Python 2.0’s 17 original error classes._

#### 2.1

Python 2.1 in April 17th, 2001 was probably as, if not more consequential than 2.0. 

It added the warning classes for message that don’t kill the program, but let the user know of potential issues. 

Not to mention, this is the first update where python could raise exceptions containing the filename and line number of a problem file. This was a **big** step forward.

#### 2.2 & 2.3

While December’s 2.2 2001 release didn’t bring much, a year a half later brought 2.3, packaged with the extremely valuable **logging** functions \[link\] for better custom error reporting, as well as a new (now extremely common) PendingDeprecationWarning being added.

#### The Zen of Python (PEP 20, 2004)

Paramount to Python’s development during this time was the the **Zen of Python**, a set of guidelines and philosophies that was always back of mind during development, released in 2004.

I found the line the line ‘Errors should never pass silently.’ quite pertinent here.

#### 2.4

March 2005 brought 2.4, with various useful but non-error related updates such as the implementation of zip().

#### 2.5

2.5, a year and a half later brought far more excitement, especially regarding exceptions.

Besides the niche introduced GeneratorExit exception, the update introduced a unified try/except/finally block \[Explain more\]. Additionally, Exceptions have had a re-write as ‘New-Style Classes’. In practice, you can now easily handle exceptions through the class system, using the newly unified try/except/finally handling, if you’d like. Here’s a [direct quote](https://docs.python.org/2/whatsnew/2.5.html) : 

> In Python 2.5, you can now write except Exception to achieve the same result, catching all the exceptions that usually indicate errors but leaving KeyboardInterrupt and SystemExit alone. As in previous versions, a bare except: still catches all exceptions.  “It’s been suggested that the bare except: form should be removed in Python 3.0, but Guido van Rossum hasn’t decided whether to do this or not.”

Raising of strings as exceptions, as in the statement raise “Error occurred”, is deprecated in Python 2.5 and will trigger a warning. The aim is to be able to remove the string-exception feature in a few releases.

Lastly, a new hidden-by-default warning, ImportWarning was introduced. It will trigger when an import sees a directory as a package but no \_\_init\_\_.py is available.

#### 2.6 & 2.7

2.6 and 2.7 were mostly considered as small, preparatory updates for python 3. Changes in these updates are pretty much exactly parallel to Python 3.

#### 3.0

Indeed, Python 3 (or Python 3000, Py3K) on the 12th month of 2008 was an big milestone for the Python community, it wasn’t that monumental. Other than removing the ‘StandardError’, and being 10% slower than Python 2.5, there was mostly changes in niche ‘annoyances and warts, and removing a lot of old ‘cruff’.

#### 3.1

3.1 introduced one of my personal favorites : Ordered Dictionaries. Nothing else of note.

#### 3.2

3.2, released almost 2 years in Febuary 2011. Despite taking more time than usual, no big updates in regardings errors and warnings. Some of note were the new ResourceWarning. It is emitted when issues with resources consumption or cleanup are detected, but is silenced unless enabled explicitly.

#### 3.3

In September 2012 brought the addition of **venv**, as well as some low level fault handlers for cpython developers. 

Not to mention, it brought in a [new I/O exception hierarchy](https://peps.python.org/pep-3151/), as explained below:

> You don’t have to worry anymore about choosing the appropriate exception type between OSError, IOError, EnvironmentError, WindowsError, mmap.error, socket.error or select.error. All these exception types are now only one: OSError. The other names are kept as aliases for compatibility reasons.

There was also mentions of better function signature reporting, but it was unclear which PEP implemented this — likely [PEP 362](https://peps.python.org/pep-0362/).

It was mentioned that with an improved error reporting system introduced in the new I/O exception hierarchy 3.3, there was hope for new improvements in error reporting elsewhere. 

#### 3.4

March 2014 3.4 update did not bring anything of note regarding errors, warnings or improved messaging.

#### 3.5

3.5 released in 2015 brought a lot of exception changes to generators, as well as two new exceptions : RecursionError \[explain\] and StopAsyncIteration \[explain\]. 

Oh, and they also made my favorite OrderedDict 4–100 times faster using asynchronous functionality.

#### 3.6

Despite 3.6 being an immense update for python users, there was only the new, now very common, ModuleNotFound error. 

This was introduced in case a user imports a module that is not available in the current environment, and there is not need for checking for ImportErrors now.

#### 3.7

June 2018’s 3.7 update had some noticeable changes. Namely some improvements in the DeprecationWarnings, making them default showable. 

Developers of Python can choose between the new future warning, versus the older depreciation warning and pending deprecation warning, for their use case \[Further explain new future warning\]. 

Lastly, improved error message reporting of ImportError displays which module by name and file when the ‘from … import … ‘ statement fails.

#### 3.8

Once again, big update in 3.8 2019 update, but not for errors and exceptions.

#### 3.9

In that same idea, 3.9 is the update known the be the last currently still fully compatible with Python 2., but no large error updates, other than changing ValueError being raised versus the new ImprotError in import statements.

#### 3.10

Python’s 3.10 (and later 3.11) updates were the juggernauts of all error and exception updates. Let’s go through the list:

* The interpreter (terminal command line) will now show the location of unclosed brackets instead of just a SyntaxError. For example:

Considerable amount of improvements in the error message reporting of errors. Some of the most notable are:

* IndentationError
* AttributeError
* NameError
* Functionality for improved line numbers for debugging tools.

#### 3.11

For 3.11, more improvements to the error locations in tracebacks (not to mention 3.11 is 10–60% faster than python 3.10)

Namely, it will now point to the exact expression that caused the error, not just the line.

To:

In probably less impactful notices, this update also made updates to exception groups and except, making Exceptions ‘enrichable’ with notes via the add\_note() method, amongst other changes.

#### 3.12

3.12 continues the hot-streak, giving us suggestions for fixing errors in NameError, ImportError and SyntaxError exceptions, like so: 

#### 3.13

3.13 in October 2024 finally released an officially free threaded python. But also, Error prompts and tracebacks have their color enabled by default, and also make them customizable through the PYTHON\_COLORS environment variables (or disables with NO\_COLOR variable).

There is also a new PythonFinalizationError exception, explained clearly [here](https://docs.python.org/3/library/exceptions.html#PythonFinalizationError).

#### 3.14 and beyond

In the future, 3.14 will bring yet another improvements in error message reporting, but the full changes are yet to be determined. Namely, when there’s an incorrect number of variables prints out the expected versus received number of variables, as such.

#### Notes and Thoughts from a Lead Python Contributor: 

It’s clear the python development team has made decisive efforts to order to improve error reporting to make the language even more user friendly, intuitive and easy to use.

Using data scraped from the ‘What’s New in Python’ update logs, visualized the number of times the word ‘error’, ‘exception’ or ‘warning’ was mentioned.

I think it tells and interesting story.

Custom Stack Barplot. Github Repo : [https://github.com/JustinBellavance/PythonDocumentationScrape](https://github.com/JustinBellavance/PythonDocumentationScrape)

Notice the sudden increase starting with Python 3.10 compared to the rest of Python 3 updates.

This is when the Python team has clearly made some priority-level changes to error messaging and reporting.

#### Why?

The recent lead-up in changes are extremely exciting, but the main question is… why? 

Why the deliberate effort to improve error messaging now?

I reached out one of the main contributors linked to these efforts, congratulated and thanked him for his recent work in improving Python error, and here’s what he had to say:

> … I want to credit the rest of the Python development team for improving error messages. It’s been a collaborative effort across many developers and releases.

I asked him two questions:

**Question:** What inspired the recent focus on improving Python’s error messages? It feels like this wasn’t a big priority before Python 3.11 — what changed?

> **Pablo Galindo Salgado:** The enhanced focus on error messages starting with Python 3.11 came from recognizing that clear, actionable error messages are crucial for both newcomers and experienced developers. Better error messages reduce debugging time and improve the overall development experience. The improvements were particularly inspired by how other modern programming languages were handling error reporting.

**Question:** Are there any plans for future improvements to Python’s error messages past 3.14? What can we look forward to?

> **Pablo Galindo Salgado:** As for future improvements beyond Python 3.14 it depends on how much time I get to some of the big items but I am focusing currently on improving debugging and profiling so probably it will just be some incremental improvements and nothing groundbreaking.

It seems confirmed that there has been a recent deliberate effort to improve Python’s error message in recent years, while keeping in mind the original philosophies for Python, like the **Zen of Python**. It will be interesting to see where Python error message go from here.

I, for one, will be keeping a very close eye on any changes.

Thank you to Pablo for taking the time out of his busy schedule to answer my questions.

This research was extremely enriching as a side-project, and I encourage anyone to really go deep into one subject that they’re passionate about. You will really learn a lot.

Software used for [analysis](https://github.com/JustinBellavance/PythonDocumentationScrape):

* Pyenv (Python 3.6.15, 3.12.7, 3.13.0)
* UV, matplotlib
* Tiobe Index
