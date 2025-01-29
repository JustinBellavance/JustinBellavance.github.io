---
date: '2025-01-20T11:50:54.000Z'
title: A Brief History of Python’s Error Messages
tagline: With comments from a leading Python contributor
preview: >-
    Suddenly appreciating the changes the Python development team has made throughout the years, I took it upon myself to dive into the archives of Python to learn all I could about the history of its errors, warnings, and messaging.
image: >-
  https://cdn-images-1.medium.com/max/1200/1*noZWO3nWvo0Ur8IqOqY9Yg.png
---
# A Brief History of Python’s Error Messages

## With comments from a leading Python contributor

It’s always been hard to ignore Python. It’s now far and away the most popular coding language, steadily surpassing classical languages such as Java and C++ in popularity.

![tiobe index](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*dMgWWKCtx64jaEuD)

[https://www.tiobe.com/tiobe-index/](https://www.tiobe.com/tiobe-index/)

Personally, I was not a programming prodigy.

Python was the first coding language I dipped my toes in when I was 16. I tried to write a basic Python script in version 3.6 and promptly gave up.

Back then, everything was overwhelming. I distinctly remember learning about errors, exceptions and warnings.

* A ‘syntax error’ likely meant I had a typo, indentation error meant I didn’t properly use python’s indentation syntax,
    
* An ‘index error’ meant I tried to access a value that wasn’t created within a list.
    
But beyond that, there was no indication or help of where my errors were happening, unless I learned some (in my opinion) complex debugging tools.

Thanks to my schoolwork and internships, I’ve persisted in truly learning Python a couple of years later. Since then, I’ve followed the Python updates throughout in my projects, going from version 3.8 to 3.13 and beyond, and finally I can say with my chest that I **love** Python.

There’s on thing that’s always bugged me, however. Between 3.6 and 3.13, Python’s error messages have gone from frustrating and confusing, to _clear, helpful_ and _intuitive_.

**And it’s not getting enough attention, nor enough credit.**

For example, see below error messages for the _exact same_ broken code below. Notice the difference between the two Python versions:

![code](https://miro.medium.com/v2/resize:fit:786/format:webp/1*NyIO8i3GZbfRNUVYsiqZHQ.png)

In Python 3.6:

![3.6 error](https://miro.medium.com/v2/resize:fit:786/format:webp/1*jRrLXPb_0gINvz8wj0hBfw.png)

and in Python 3.12:

![3.12 error](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*DrBkIRvW71LLEZKC5E5YGA.png)


You see, maybe I wouldn’t have given up on programming all those years back if I started with Python 3.12 instead of 3.6.


### The History of Python Error Messages

Suddenly appreciating the changes the Python development team has made throughout the years, I took it upon myself to dive into the archives of Python to learn all I could about the history of its errors, warnings, and messaging.

Here’s what I found:


### Pre Python 2.0

Python was the creation of Guido van Rossum’s. It was heavily based on the [ABC programming language](https://en.wikipedia.org/wiki/ABC_(programming_language)), created at his time at the [Centrum Wiskunde & Informatica (CWI)](https://www.cwi.nl/en/).

Version 1.0.0 was technically first released in 1994.

Even back then, Python’s creator had strict guidelines for the development of Python’s error handling (from his [2009 blog post](https://python-history.blogspot.com/2009/01/pythons-design-philosophy.html)):

> Errors should not be fatal. That is, user code should be able to recover from error conditions as long as the virtual machine is still functional.

> At the same time, errors should not pass silently (These last two items naturally led to the decision to use exceptions throughout the implementation.)

> A bug in the user’s Python code should not be allowed to lead to undefined behavior of the Python’s interpreter; a core dump is never the user’s fault.

In Python, errors and user-given warnings are known under the umbrella term _exceptions._

As of python 3.13.0, there are 37 different errors types, with 11 warnings types. I found an great explainer by Andrei Maksimov [here](https://hands-on.cloud/python-exceptions/) (2021).

![hierarchy](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*7ajjDa74hnKdLDh_.png)

These are all objects that help inform user on potential bugs or incompatibilities within their code the might prevent them from achieving their wanted behavior.

This exception hierarchy has changed **a lot** since the birth of Python, as seen in the Python 2.7.18 example above.


### 2.0 (October 2000)

With this in mind, development of Python continued.

When it came time to Python’s open-source 2.0 release (away from [CNRI](https://en.wikipedia.org/wiki/Corporation_for_National_Research_Initiatives)) in 2000, two new subclasses were defined: the _TabError_ and _IndentationError_, subsets of the previously stand-alone _SyntaxError_.

With this, the basic hierarchy of errors were first defined, making it so no error would ever pass undefined — there would always be a controllable exception for each Python error situation.

*   **StandardError** (Base class for built-in exceptions that are not system-exiting):
    
*   **ArithmeticError** (Base class for arithmetic exceptions):
    
*   **OverflowError**: Raised when a numerical result exceeds the maximum limit for a numeric type.
    
*   **ZeroDivisionError**: Raised when division or modulo by zero occurs.
    
*   **FloatingPointError**: Raised when a floating point operation fails.
    
*   **LookupError** (Base class for indexing errors)
    
*   **IndexError**: Raised when a sequence subscript is out of range.
    
*   **KeyError**: Raised when a dictionary key is not found.
    
*   **EnvironmentError** (Base class for I/O related errors):
    
*   **IOError**: Raised when an I/O operation (such as file opening) fails.
    
*   **OSError**: Raised for OS-related errors, such as “file not found” or “access denied.”
    
*   **EOFError**: Raised when the input() or raw\_input() functions hit an end-of-file condition.
    
*   **ImportError**: Raised when an import statement fails to find the module definition.
    
*   **MemoryError**: Raised when an operation runs out of memory.
    
*   **NameError**: Raised when a local or global name is not found.
    
*   **UnboundLocalError**: A subclass of NameError, raised when a local variable is referenced before assignment.
    
*   **ReferenceError**: Raised when a weak reference is used to access an object that has been garbage collected.
    
*   **RuntimeError**: Raised when an error is detected that doesn’t fall in any of the other categories.
    
*   **NotImplementedError**: A subclass of RuntimeError. Raised when an abstract method is called that is not implemented.
    
*   **SyntaxError**: Raised when the parser encounters a syntax error.
    
*   **IndentationError** (Introduced in Python 2.0): A subclass of SyntaxError, raised when indentation is incorrect.
    
*   **TabError** (Introduced in Python 2.0): A subclass of IndentationError, raised when tabs and spaces are mixed in indentation.
    
*   **TypeError**: Raised when an operation or function is applied to an object of inappropriate type.
    
*   **ValueError**: Raised when a function receives an argument of the correct type but an inappropriate value.
    
*   **UnicodeError**: A subclass of ValueError. Raised when a Unicode-related encoding or decoding error occurs.
    
*   **AttributeError**: Raised when an attribute reference or assignment fails.
    
*   **SystemError**: Raised when the interpreter finds an internal error, but the situation is not critical enough to make it exit.
    
*   **AssertionError**: Raised when an assert statement fails.
    
*   **StopIteration**: Raised to signal the end of an iterator’s items (used to stop loops).
    

_Python 2.0’s 17 original error classes._


### 2.1 (April 2001)

Python 2.1 in April 17th, 2001 was probably as, if not more consequential than 2.0.

It was the update to add the **warning classes** for messages to the user that don’t kill the program, but instead let them know of potential issues.

Not to mention, this is the first update where python could raise exceptions containing the filename and line number of a problem file. This was a **big** step forward.


### 2.2 & 2.3 (December 2001, July 2003)

While December’s 2.2 release didn’t bring much, two and a half years later brought 2.3, packaged with the extremely valuable [logging functions](https://docs.python.org/2/whatsnew/2.3.html#pep-282-the-logging-package) for better custom error reporting, as well as a new (now extremely common) _PendingDeprecationWarning_ being added.


### The Zen of Python (PEP 20, 2004)

Paramount to Python’s development during this time was the the **Zen of Python**, a set of guidelines and philosophies that was always back of mind during development, released in 2004.

![zen of python](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*R3yEorD9d5prHb9f.png)

I found the line the line ‘Errors should never pass silently.’ quite pertinent here.


### 2.4 (March 2005)

Version 2.4 brought came with various useful but non-error related updates such as the implementation of zip().


### 2.5 (September 2006)

Version 2.5 brought far more excitement a year and a half later, especially regarding exceptions.

Besides the niche (my opinion) introduced _GeneratorExit_ exception, the update introduced a unified [try/except/finally block](https://edoras.sdsu.edu/doc/Python-Docs-2.5/whatsnew/pep-341.html), improving error handling for developpers.

Additionally, Exceptions have had a re-write as ‘New-Style Classes’. In practice, you can now easily handle exceptions through the class system, using the newly unified try/except/finally handling, if you’d like. Here’s a [direct quote](https://docs.python.org/2/whatsnew/2.5.html) :

> In Python 2.5, you can now write except Exception to achieve the same result, catching all the exceptions that usually indicate errors but leaving KeyboardInterrupt and SystemExit alone. As in previous versions, a bare except: still catches all exceptions.  “It’s been suggested that the bare except: form should be removed in Python 3.0, but Guido van Rossum hasn’t decided whether to do this or not.”

> Raising of strings as exceptions, as in the statement raise “Error occurred”, is deprecated in Python 2.5 and will trigger a warning. The aim is to be able to remove the string-exception feature in a few releases.

Last but not least, a new hidden-by-default warning, _ImportWarning_ was introduced. It will trigger when an import sees a directory as a package but no \_\_init\_\_.py is available.


### 2.6 & 2.7 (October 2008, July 2010)

2.6 and 2.7 were mostly considered as small, preparatory updates for the 3rd version of Python. Changes in these updates are pretty much exactly parallel to Python 3.


### 3.0 (December 2007)

While Python Version 3.0 (or Python 3000, Py3K) on the 12th month of 2008 was an big milestone for the Python community, it wasn’t that monumental for error messaging.

Other than removing the ‘StandardError’, and being 10% slower than Python 2.5, there was mostly changes in niche “annoyances and warts, and removing a lot of old cruff”.


### 3.1 (June 2009)

Version 3.1 introduced one of my personal favorites : Ordered Dictionaries. Nothing else of note.


### 3.2 (February 2011)

Version 3.2, released almost 2 years in February 2011. Despite taking more time than usual, no big updates regarding errors and warnings.

Some of note were the new _ResourceWarning —_ emitted when issues with resources consumption or cleanup are detected, but is currently silenced unless enabled explicitly.


### 3.3 (September 2012)

Version 3.3 brought the addition of **venv**, as well as some low level fault handlers for cpython developers.

Not to mention, it brought in a [new I/O exception hierarchy](https://peps.python.org/pep-3151/), as explained below:

> You don’t have to worry anymore about choosing the appropriate exception type between OSError, IOError, EnvironmentError, WindowsError, mmap.error, socket.error or select.error. All these exception types are now only one: OSError. The other names are kept as aliases for compatibility reasons.

There was also mentions of better function signature reporting, but it was unclear which PEP implemented this — likely [PEP 362](https://peps.python.org/pep-0362/).

It was mentioned that with an improved error reporting system introduced in the new I/O exception hierarchy from version 3.3, there was hope for new improvements in error reporting elsewhere.


### 3.4 (March 2014)

Version 3.4did not bring anything of note regarding errors, warnings or improved messaging.


### 3.5 (September 2015)

3.5 released in 2015 brought a lot of exception changes to generators, as well as two new exceptions : [_RecursionError_](https://github.com/python/cpython/issues/63434) and a a change in [_StopIteration_](https://peps.python.org/pep-0479/) in generators.

Oh, and they also made my favorite OrderedDict 4–100 times faster using asynchronous functionality.


### 3.6 (December 2016)

Despite 3.6 being an immense update for python users, there was only the new, now very common, _ModuleNotFound_ error introduced.

This was developed in the case where a user imports a module that is not available in the current environment, and there is not need for checking for _ImportErrors_ now.


### 3.7 (June 2018)

June 2018’s 3.7 update had some noticeable changes. Namely some improvements in the _DeprecationWarnings_, making them default showable.

Developers of Python can choose between the new future warning, versus the older depreciation warning and pending deprecation warning, for their use case.

Lastly, improved error message reporting of _ImportError_ displays which module by name and file when the ‘from … import … ‘ statement fails, which is quite common amongst new Python users.


### 3.8 (October 2019)

Once again, version 3.8 was a large and consequential, but with no love for errors, exceptions and warnings.


### 3.9

Version 3.9 is the update known to be the last version still fully compatible with Python 2, but no large error updates, other than deprecating the _ValueError_ being raised versus the new _ImportError_ in import statements.


### 3.10

Python’s 3.10 (and later 3.11) updates were the sudden juggernauts of all error, exception and warning updates.

*   The interpreter (terminal command line) will now show the location of unclosed brackets instead of just a SyntaxError. For example:
    
![interpreter example](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*U97ZogKfpVi7QVcK)

Considerable amount of improvements in the error message reporting of errors. For specific errors, error messages will now show the specific line of error, instead of some higher level function. Some of the most notable are:

*   _IndentationError_
    
*   _AttributeError_
    
*   _NameError_

Not to mention, functionality has been widely improved for line numbers for certain debugging tools.


### 3.11

For 3.11, more improvements to the error locations in tracebacks (not to mention 3.11 is 10–60% faster than python 3.10)

Namely, it will now point to the exact expression that caused the error, not just the line.

![before](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*768WLOM1sFKMpT8z)

To:

![after](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*fFJLGXuhtlD_0EIL)

In probably less impactful changes, this update also made updates to exception groups and _except_, making exceptions ‘enrichable’ with notes via the add\_note() method, amongst other changes.


### 3.12

3.12 continues the hot-streak, giving us suggestions for fixing errors in _NameError_, _ImportError_ and _SyntaxError_ exceptions, like so:

![did you forget](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*Sq7_yuhNoW_nXhvg)


### 3.13

3.13 in October 2024 finally released an officially free threaded python.

Also, error prompts and tracebacks have their color enabled by default, and also make them customizable through the PYTHON\_COLORS environment variables (or disabled with the NO\_COLOR variable).

There is also a new _PythonFinalizationError_ exception, explained clearly [here](https://docs.python.org/3/library/exceptions.html#PythonFinalizationError).


### 3.14 (and beyond)

In the future, 3.14 will bring yet another improvements in error message reporting, but the full changes are yet to be determined. Namely, when there’s an incorrect number of variables prints out the expected versus received number of variables, as such.

![unpack 3.14](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*QXsOaVgPCmqfuTor)

### Notes

It’s clear the python development team has made decisive efforts to order to improve error reporting to make the language even more user friendly, intuitive and easy to use.

Using data scraped from the ‘What’s New in Python’ update logs, visualized the number of times the word ‘error’, ‘exception’ or ‘warning’ was mentioned.

I think it tells and interesting story.

![errors, exception, warnings](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*noZWO3nWvo0Ur8IqOqY9Yg.png)

Custom Stack Barplot. Github Repo : [https://github.com/JustinBellavance/PythonDocumentationScrape](https://github.com/JustinBellavance/PythonDocumentationScrape)

Notice the sudden increase starting with Python 3.10 compared to the rest of Python 3 updates.

This is when the Python team has clearly made some priority-level changes to error messaging and reporting.

That being said, no one truly knows what the future holds for future Python versions, even a lead contributor.

### Answers from a lead Python contributor

The recent lead-up in changes are extremely exciting, but the main question is… why?

Why the deliberate effort to improve error messaging now?

I reached out one of the main contributors linked to these efforts, congratulated and thanked him for his recent work in improving Python error, and here’s what he had to say:

> … I want to credit the rest of the Python development team for improving error messages. It’s been a collaborative effort across many developers and releases.

I asked him two main questions:


**Question:** What inspired the recent focus on improving Python’s error messages? It feels like this wasn’t a big priority before Python 3.11 — what changed?

> **Pablo Galindo Salgado:** The enhanced focus on error messages starting with Python 3.11 came from recognizing that clear, actionable error messages are crucial for both newcomers and experienced developers. Better error messages reduce debugging time and improve the overall development experience. The improvements were particularly inspired by how other modern programming languages were handling error reporting.


**Question:** Are there any plans for future improvements to Python’s error messages past 3.14? What can we look forward to?

> **Pablo Galindo Salgado:** As for future improvements beyond Python 3.14 it depends on how much time I get to some of the big items but I am focusing currently on improving debugging and profiling so probably it will just be some incremental improvements and nothing groundbreaking.


It seems confirmed that there has been a recent deliberate effort to improve Python’s error message in recent years, while keeping in mind the original philosophies for Python, like the **Zen of Python**. It will be interesting to see where Python error message go from here.

I, for one, will be keeping a very close eye on any changes.



Thank you to Pablo for taking the time out of his busy schedule to answer my questions.

This research was extremely enriching as a side-project, and I encourage anyone to really go deep into one subject that they’re passionate about. You will really learn a lot.

Software used for [analysis](https://github.com/JustinBellavance/PythonDocumentationScrape):

*   Pyenv (Python 3.6.15, 3.12.7, 3.13.0)
*   UV, matplotlib
*   Tiobe Index

All the best,
W
Justin