# A FAQ for Perl 7

Answers to your questions about Perl 7.

## What's Perl 7?

Perl 7 is Perl v5.32 with saner, more modern defaults. It's a transitional major version before we get to breaking changes.

There's a [Perl 7 proposal](https://github.com/Perl/perl5/wiki/The-Proposal-for-Perl-7) in the wiki for the [`perl5` repo](https://github.com/Perl/perl5/).

## Why not Perl 32 (or 34)?

There was some thought to dropping the 5 from the version and using what we already think of as the major version. However, that would reinforce the idea that it's just a continuation of the Perl 5 line. And, 32 is a big number. 

We could have done many things, but we had to choose one of them. Perl 7 is what we chose.

## What are the new defaults?

We don't know for sure because we don't have Perl 7 yet. These are some of the things already on the list, although there's no guarantee on anything yet:

* enable strict by default
* enable warnings by default
* disable bareword filehandles
* disable multidimensional array emulation (a Perl 4 trick)
* enable subroutine signatures
* change prototypes to use the `:prototype` attribute

## When will this happen?

In his announcement at The Perl Conference in the Cloud, Sawyer X (Perl's project lead) said they'd like to have it within a year, but maybe sooner than that.

## Will Perl 7 run my Perl 5 code?

Most likely it will. Perl 7 is Perl 5.32 with different defaults. If your code can run under v5.32, you are probably close to ready. Note that in the past several years, Perl 5 has removed features that were deprecated even when v5.0 was released in 1994. If you are using those, you need to fix that. Trying your code under v5.32 will find those problems for you.

There will be some compatibility modes. This may be as simple as:

    use compat::p5;
    
But, since Perl 7 is v5.32, you already know how to turn off defaults you don't like:

    no strict;
    
    { no warnings; ... }
    
Don't rely on these as a crutch though. If you want to stick to Perl 5 behavior, you can still use Perl 5.

## What happens to Perl 5?

Perl 5 goes into long term maintenance. That can be as long as a decade or more. You'll still get important security and bug fixes, just for a little bit longer than usual.

The current [Perl support policy](https://perldoc.perl.org/perlpolicy.html) guarantees support for the previous two maintenance releases. With a new maintenance release every year, this effectively means two years of support for a major release (such as v5.30 and v5.32).

## What will `/usr/bin/perl` be?

We don't know the answer to this one yet. `/usr/bin/perl` is the system Perl. For at least a decade, I have been telling people not to use the system `perl` for user code.  This is the `perl` that the system employs to handle system Perl programs. So, that system can choose what they need. We are working with major packagers to figure out what works best. On my macOS box, that's v5.18 (and soon [won't be there at all](https://developer.apple.com/documentation/macos_release_notes/macos_10_15_beta_release_notes)), but they are also taking it away. 

Relying on the system means you let someone else make the decision for you, and it's a bigger problem than migrating to Perl 7, or even Perl at all. Let's say that your system provides an out-of-date `perl`, which is not uncommon. Then you update to v5.26. Now your regexes break because you have an [unescaped left brace](https://www.effectiveperlprogramming.com/2017/04/you-must-escape-the-left-brace-in-a-regex/). Since you didn't control a key aspect of your user application, you didn't control the system decision to break your code. People often find these issues after a system upgrade (planned or otherwise). 

Having said that, my guess is that we'll have something close to the Python situation, where there's `python`, `python2`, and `python3`. So, we'd have `perl` (whatever the system needs, likely the same thing they are using now), `perl5` (a symlink to `perl`), and `perl7` (A different binary). That's just my guess based on how I've seen these things work elsewhere.

The Perl module paths are already set up for this too. We can put the version right in the `@INC` paths so two different versions can install modules into the same prefix (say, `/usr/lib/perl`) without conflicting with each other. Or they could simply use different prefixes.

As the user, your decision is likely made for you. If you aren't going to install your own `perl` for your application, you're stuck on whatever the system provides. If you do install your own `perl`, you get to decide how that happens.

## What happens if Perl 7 doesn't happen?

That's the gorilla-elephant hybrid in the room, isn't it? We did this once in 2000, didn't we? Perl 6 didn't turn out how we thought it would, but that's life sometimes.

If Perl 7 doesn't happen, we get Perl v5.34 and keep doing that.

But, it's very unlikely that we'll fail here. Perl 7 is v5.32. We already have all of the code. This is more paper shuffling and administrative work than anything else. The Perl community already has the tools in place to test all of CPAN against any Perl release (I know, I get the emails about my modules being broken). Perl 7 is more about process adjustment than new code.

And, consider this: Perl finally moved to GitHub. It converted all of its reports in Request Tracker to GitHub issues. You can now interact with the [Perl repo on GitHub](https://github.com/Perl/perl5). That was a huge project, and it's the same people that made it happen.

Honestly, Perl 6 was announced without a plan. I was there (in the room) when we decided to invent it. Larry Wall announced the new direction that week with no plan, and called it "the community's rewrite of Perl". A long RFC process followed, which [Mark Jason Dominus summarized for Perl.com](https://www.perl.com/pub/2000/11/perl6rfc.html/).

This is different. Key people have been planning this for a year. They've carefully considered how big a bite they can take, and have a modest plan going into the next year. The code is already all there.

## What happens to filehandles if indirect object notation disappears?

Some people realize that `print` and friends can be methods on the filehandle. Have you ever considered why there's no comma after the filehandle?

    print STDOUT "Hello world!\n";
    STDOUT->print( "Hello world!\n" );
    
So far, filehandles seem to be safe under `no feature qw(indirect)`.

## When will feature X be included?

Perl 7 is v5.32 with different defaults. You won't see new features and you won't have any taken away from you if you're running on v5.32. If it's already in Perl, you can have it. If it isn't, probably not.

There are many things that people want, and I expect that Perl 8 will be the version that handles that. Perl 7 sets the stage for completely breaking with Perl 5 compatibility, but Perl 8 will be the major version that can actually do it.

## Will Perl 7 have a new object system?

There's the possibility of a new object system. Many people are interested in Ovid's [Cor proposal](https://github.com/Ovid/Cor). But, by "new", we really often mean syntactic sugar over what is already in the codebase. Since Perl 7 is compatible with v5.32, you aren't going to lose the way that Perl does it now.

## Will UTF-8 features be enabled by default?

Maybe. Let's see how much work that is. We'd all like to have this, but there's death and destruction in the wake of a big switch like that. Perl has all the features it needs to handle that, but we don't know how much of the community is ready for that.

But, this is not simply enabling some features. Changing the default behavior of encodings is likely to break many programs because the program itself needs to be ready for Unicode (there's a primer in an appendix to the latest [Learning Perl](https://www.learningperl.com). Tom Christiansen answered [Why does modern Perl avoid UTF-8 by default?](https://stackoverflow.com/a/6163129/2766176).

## What about Perl 6?

Perl 6 started as an ambitious effort to completely rewrite Perl. For various reasons, that didn't replace Perl and went off to live a separate life as the language now known as [Raku](https://www.raku.org). The number 7 was next in line.

## So when's Perl 8 coming out?

One major version at a time! Let's figure out Perl 7 first.

## What about the other forks of Perl?

Will Braswell does an amazing job of outlining the paths of various offshoots of Perl in his talk [The Perl Family Tree](https://vimeo.com/394230613).

Perl 6 happened, then struck out on its own as Raku.

The community has talked about a Perl 7 since at least 2013. One brave soul even made a [toy project on GitHub](https://www.github.com/perl7), but that was never a serious attempt. It would have been based on NQP (Not Quite Perl), which would have made it compilable to MOAR, the engine that powers Raku.

Similarly, there was a thing called [Perl 11](http://perl11.org), which was more an umbrella for a design philosophy behind several exploratory forks of Perl. These sort of projects let people try heterodox ideas, and that's fine. They just aren't `perl`.

## How can I find out more about Perl 7?

* [Getting Better, Not Getting By](https://www.youtube.com/watch?v=6wPMh-3qYJM), Sawyer's keynote at The Perl Conference in the Cloud
* [Sawyer's Announcement on p5p](https://www.nntp.perl.org/group/perl.perl5.porters/2020/06/msg257565.html)
* [Announcing Perl 7](https://www.perl.com/article/announcing-perl-7/) on Perl.com
* [Perl 7 tl;dr](http://blogs.perl.org/users/brian_d_foy/2020/06/the-perl-7-tldr.html)
* [Preparing for Perl 7](https://leanpub.com/preparing_for_perl7), from [Perl School](https://perlschool.com)
* [The Proposal for Perl 7](https://github.com/Perl/perl5/wiki/The-Proposal-for-Perl-7)
