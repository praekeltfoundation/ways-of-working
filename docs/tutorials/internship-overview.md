# Internship Overview

## Our Programming Language of Choice
Praekelt is primarily a Python shop. If you feel like you need a python refresher, I'd recommend doing a few online programming challenges to help remember some of the syntax structure. I use [Coderbyte](http://coderbyte.com/), but there are a [ton of options](http://codecondo.com/coding-challenges/) out there.

## OK, I can code, but how does the Internet work?
When I started as an intern at Praekelt, I knew how to program relatively small things like getting the palindromic primes between two numbers. It turns out that this is not particularly useful when you're supposed to work on a website. Pretty much everything we do is connected in some way to the web and web technologies. If you're familiar with things like frameworks, HTML, Javascript and CSS, that's great. If not, that's also OK. Like me, you'll pick this stuff up as you go along. If there's something you don't understand, particularly in the first couple weeks, take your time and use Google, YouTube and other interns or devs to explain this stuff to you.

## Code style
If a bunch of people are writing and collaborating on code, it helps if there's a uniform style that everyone uses. We use [pep8](https://www.python.org/dev/peps/pep-0008) for our python code. We're pretty strict about it, in fact your builds will fail within the automated testing environment if you've failed to comply, like leaving trailing whitespace . This can be pretty frustrating, so get yourself an add-on to your text editor or IDE (like [this](https://github.com/SublimeLinter/SublimeLinter-pep8) or [this](https://atom.io/packages/pep8)) to check your code for mistakes or things that need to change. This takes the hassle out of learning all of the conventions and will make your life a lot easier.

You'll also note that there are very few comments in our code. I was surprised to find this out after having been told time and time again that comments are reeeeally important. Basically, the approach here is that you should be naming your variables and writing your code in such a way that it is easy to understand and doesn't need additional commentary. You'll also notice that names/dates/headers, that kind of thing, are all left out of the code. Github already has that meta-information. We don't need to repeat ourselves repeat ourselves.

## Testing
Our approach to development is that if you haven't written tests for your code, you're only half done. We test everything we write and as you get going with us, you'll be expected to write tests that will test every part of your code. This means thinking about standard cases, edge cases and points of failure and recovery. The good news is that we have some excellent tools to help us with testing. You will run tests locally, but we also use tools like [Travis](https://travis-ci.org/) and [Coveralls](https://coveralls.io/) so that every time you push code to Github, the code is tested all over again, showing you when a build fails, where it fails and if parts of your code are not tested. We compartmentalize our tests in what are called [unit tests](http://searchsoftwarequality.techtarget.com/definition/unit-testing) and with any changes you've made, Travis will run all of those tests again to make sure that stuff has not been broken with your changes. In fact, there is even [an approach to coding](http://en.wikipedia.org/wiki/Test-driven_development) where you write failing tests first and then write code to get the tests passing. You don't have to do that, but it's worth checking out. The specific testing packages that you use will depend on what you work on.

## Some concepts
There are a couple of concepts/ideas/technologies/stuff that you should get comfortable with:

- How to use the terminal or command line, [here's](https://github.com/jlevy/the-art-of-command-line) a helpful resource for the command line, although it is centered toward Linux users.
- Git and version control, which is dealt with in the next article
- Web frameworks and what they are. I found [this article](http://en.wikipedia.org/wiki/Web_application_framework) and [this video](https://www.youtube.com/watch?v=b3p4rBZAwwE) helpful. The web applications that we use are [Django](https://www.djangoproject.com/) and [Wagtail](https://wagtail.io/) among others. Don't worry, you'll be given a lot of time to familiarize yourself with these technologies.

## In summary
* We like Python
* There's a fair bit of stuff to learn, but it's OK, you'll get there
* We adhere to a certain code format called pep8
* We test our code. A lot.
* We don't expect you to know all of this stuff from the beginning
