# A FAQ for Perl 7

Answers to your questions about Perl 7.

## What's Perl 7

Perl 7 is Perl v5.32 with saner, more modern defaults. It's transitional major version before we get to breaking changes.

## Why not Perl 32 (or 34)?

There was some thought to dropping the 5 from the version and using what we already think of as the major version. However, that would reinforce the idea that it's just a continuation of the Perl 5 line. And, 32 is a big number. 

We could have done many things, but we had to choose one of them. Perl 7 is what we chose.

## What's are the new defaults?

We don't know for sure because we don't have Perl 7 yet. These are some of the things already on the list, although there's no guarantee on anything yet:

* enable strict by default
* enable warnings by default
* disable bareword filehandles
* disable multidimensional array emulation (a Perl 4 trick)
* enable subroutine signatures
* change prototypes to use the `:prototype` attribute

## When will this happen?

In his annoucement at The Perl Conference in the Cloud, Sawyer X (Perl Project Lead) said they'd like to have it within a year, but maybe sooner than that.

## Will Perl 7 run my Perl 5 code?

Most likely it will. Perl 7 is Perl 5.32 with different defaults. If your code can run under v5.32, you are probably close to ready. Note that in the past several years, Perl 5 has removed features that were deprecated even when v5.0 was released in 1994. If you are using those, you need to fix that. Trying your code under v5.32 will find those problems for you.

## When feature X be included?

Perl 7 is v5.32 with different defaults. You won't see new features and you won't have any taken away from you if you're running on v5.32. If it's already in Perl, you can have it. If it isn't, probably not.

There are many things that people want, and I expect that Perl 8 will be the version that handles that. Perl 7 sets the stage for completely breaking with Perl 5 compatibility, but Perl 8 will be the major version that can actually do it.

## Will Perl 7 have a new object system?

There's the possibility of a new object system. Many people are interested in Ovid's [Cor proposal](https://github.com/Ovid/Cor). But, by "new", we really often mean syntactic sugar over what is already in the code base. Since Perl 7 is compatible with v5.32, you aren't going to loose the way that Perl does it now.

## Will UTF-8 features be on by default?

Maybe. Let's see how much work that is. We'd all like to have this, but there's death and destruction in the wake of a big switch like that. Perl has all the features it needs to handle that, but we don't know how much of the community is ready for that.

But, this is not simply enabling some features. Changing the default behavior of encodings is likely to break many programs because the program itself needs to be ready for Unicode (there's a primer in an appendix to the latest [Learning Perl](https://www.learningperl.com). Tom Christainsen answered [Why does modern Perl avoid UTF-8 by default?](https://stackoverflow.com/a/6163129/2766176).

## What about Perl 6?

Perl 6 started as an ambitious effort to completely rewrite Perl. For various reasons, that didn't replace Perl and went off to live a separate life as the language now known as [Raku](https://www.raku.org). The number 7 was next in line.

## So when's Perl 8 coming out?

One major version at a time! Let's figure out Perl 7 first.

## How can I find out more about Perl 7?

* [Getting Better, not Getting By](https://www.youtube.com/watch?v=6wPMh-3qYJM), Sawyer's keynote at The Perl Conference in the Cloud
* [Announcing Perl 7](https://www.perl.com/article/announcing-perl-7/) on Perl.com
* [Perl 7 tl;dr](http://blogs.perl.org/users/brian_d_foy/2020/06/the-perl-7-tldr.html)
* [Preparing for Perl 7](https://leanpub.com/preparing_for_perl7), from [Perl School](https://perlschool.com)
