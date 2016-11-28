# Preface
I am not a lawyer. Even if you find language
that sounds legalize within, this is not legal advice. 
This document describes the various ways
in which open source software developers organize and attribute their work from a 
copyright and licensing perspective. The emphasis here is on the internal organization
of the artifacts (code, documentation, agreements, etc), not the external representation.
More specifically, we can think of an open source project as having a means for consuming
incoming changes and a means to produce artifacts for usage. From a licensing and agreement
perspective this document describes the incoming set of rules (the 
"contribution model"), which are not always the same as the outgoing set (the "licensing model").

At the end of this document, we'll discuss why we have chosen a particular
contribution model ("In == Out, DCO pull request")
for our projects.

A word of caution: if you google around, you'll find many different and contradictory 
explanations of this subject. Most of it is authored by non-lawyers (including this one!).
That's just the nature of the internet. Read everything with a critical eye.

# Target Audience
If you are the owner of an open source project, this document might help you
choose a contribution model for your project.
If you want to contribute to an open source project, this document might help
you understand your rights and responsibilities with respect to the contribution
model chosen by the project you want to contribute to.

You should think about this document as a layman's attempt to describe to other lay-folk 
the basic features of contribution models.

# Open Source Contribution Models

There are 4 main models, with some sub-varieties in each. Roughly in historical order, these are:

1. Copyright assignment agreement (CAA)
2. Contribution license agreement (CLA)
3. In == Out
4. In == Out with developer certificate of origin (DCO)

In all of these, there is one shared concern: if person X writes some code Y, 
who owns the copyright to code Y before it's contributed? 
In many cases, the answer is not person X,
because person X may (knowingly or not) have entered into a contract
(for example, an employment agreement under US law) that assigns copyright
to someone else. The full extent of this is beyond the scope of this document.

From a legal perspective, the contribution (and any implied or explicit agreements)
must be authorized by the copyright holder, which is not necessarily the code
author. In the remainder of this document, we'll assume the copyright holder is 
agreeing through the actions of the actual contributor. Many of the procedures
below are bifurcated between a "contributor is copyright holder" vs. a 
"contributor represents the copyright holder" procedures.

## Copyright Assignment 
In this case, the copyright holder enters into an agreement with the product owner
to assign copyright to the product owner. This assignment form typically contains language
like: 
```
I, NAME OF PERSON, hereby transfer to the NAME OF FOUNDATION my entire right, title,
and interest (including all rights under copyright) in my changes and enhancements 
to the program NAME OF PROGRAM,
```

Free Software Foundation (FSF) copyrighted
packages work under this model. FSF provides justification for this 
[choice](https://www.gnu.org/licenses/why-assign.en.html).

Copyright assignment is generally considered the most restrictive of all the 
contribution models for the contributor. If not worded carefully, it may strip the original
author of all rights to the code. It is the most empowering model for the project owner. 

## Contribution License Agreement
A contribution license agreement is an agreement between the contributor and the
project owner that gives the project owner certain rights and privileges, typically
well beyond the project license. Let's make that clear with an example: Apache 
foundation requires individual and corporate CLA's signed by contributors to its projects.
The Apache 2.0 [License](https://www.apache.org/licenses/LICENSE-2.0) differs from
the [contribution agreement](https://www.apache.org/licenses/icla.txt) 
for someone contributing code to Apache.
Specifically, there are two substantive differences:

1. Apache 2.0 license has a large "Redistribution" clause (#4). Someone consuming
software under Apache 2.0 has to abide by all these rules, but Apache foundation
has no such restrictions in using code that was contributed to it. You can think of
this as a super-permissive incoming license: the contributors are putting code in under
a BSD-like license, and Apache is free to incorporate that into an Apache licensed code base.
2. In the contribution agreement, the contributor is attesting to certain things
such as the origin of the code and the contributor's legal rights to contribute such code.

The asymmetry in this arrangement can be source of contention and CLA's can be considered
heavy-weight. 
[OpenStack](https://wiki.openstack.org/wiki/OpenStackAndItsCLA#OpenStack_and_its_Contributor_License_Agreement)
and 
[Chef](https://blog.chef.io/2016/09/19/introducing-developer-certificate-of-origin/)
are examples of projects that have switched from CLA's to DCO (described below).

## In == Out
When the incoming contributor code is licensed under the same license as the outgoing artifacts, 
the model is called "In == Out" (
The Linux kernel used to be under this model, but after the legal wrangling with 
[SCO](http://lkml.iu.edu/hypermail/linux/kernel/0405.2/1301.html), 
they adopted a "In == out with DCO" (described below) model.

While this is clearly the most light weight and equitable model, it may not provide
the kinds of legal protection that a project owner might want.

Even for licenses like Apache 2.0, which have an explicit contribution clause, 
there is some notion that there should be some explicit acknowledgement:

[Rick Clark](https://lists.launchpad.net/openstack/msg06467.html) on OpenStack history:
```
IANAL, but I was told by lawyers when we were in the planning stages of
starting Openstack, that while in the US submitting code under the
Apache License 2.0 was enough to bind the submitter to it, that is not
the case in all countries.  Some countries require explicit acceptance
to be bound by it.
```
## In == Out with Developer Certificate of Origin (DCO)
As discussed above, In == Out can be considered insufficient for providing
legal protection. The Developer Certificate of Origin (DCO) was introduced to
make the following two points explicit:
1. The contributor attests that they are legally entitled to make the contribution
under the Out license.
2. The contributor agrees that everything about this interaction is essentially public
(under the terms of the license) and kept forever.
The second point is necessary because of European 
[retention laws](http://www.linuxtoday.com/developer/2005061402426OSKNDV),
and we'll leave it at that.

So how does a contributor agree to the DCO? There are two common methods
for that: implicit and explicit.

With implicit acceptance, the contribution procedures for the project reference
the DCO and the contributor adds a line to every commit that says:
```
Signed-off-by: Random J Developer <random@xxxxxxxxxxxxx>
```
It's not really clear how a line like that on a code commit establishes acceptance of another document, 
so some projects opt for explicit acceptance. This usually entails some sort of 
email, snail mail or click through acceptance, plus the ```Signed-off-by:``` commit message.

# Comparing the 4 models:
We can roughly rate these different models along three criteria:

1. Equitability: how symmetric is rights of a contributor compared to 
the project owner?
2. Bureaucracy: how much work is it for a contributor to be on-boarded
and continue to contribute?
3. Legal protection: how much legal protection does the model provide?
Note that these ratings are neither vetted by a lawyer, nor tested in 
a court of law.

| Contribution Model             | Equitability | Bureaucracy   | Legal protection |
|--------------------------------|--------------|---------------|------------------|
| Copyright Assignment           | Low          | High          | High             |
| Contributor License Agreement  | Medium       | Medium - High | Medium           |
| In == Out                      | High         | None          | Low              |
| In == Out with DCO             | High         | Low - High    | Medium           |

# The Transfer and Storage Problem
With any sort of explicit agreement or contract, the acceptance must be somehow documented.
There are two things to consider here: how is the information transfered, and once transfered, 
how is it stored?

Older procedures required paper copies to be signed and mailed in. Clearly in this case,
the agreement was stored separately from the code.

Newer procedures span the gamut of electronic methods from sending an email to clicking on a button
on a web page. Most of these methods still store the document separately from the code.

If we consider the agreement and its acceptance to be just data, we recognize that such data
is not different in form from a code contribution (although it is very different in content).
Since code also has to be transfered and stored, we therefore have 4 choices (not considering
cases where there are multiple ways of achieving each):

1. Different transfer, different storage compared to code.
2. Different transfer, same storage compared to code.
3. Same transfer, different storage compared to code.
4. Same transfer, same storage compared to code.

Oddly, the most common case is (1). For example, it's nearly impossible for an outside party
to know who has signed a contribution agreement with the FSF (CAA), 
the Apache foundation (CLA) or the Eclipse foundation (DCO).
In the long term, this can become a problem, as projects join a foundation or move
away, or the foundation changes (split, merge, cease to exist), or when a project
itself changes its contribution model.

Choice (4), where the transfer and storage of the document are the same as code has the
advantage that as long as the code is around, the agreements that went into creating 
that code are also available. An example of this is our "In == Out, DCO pull request" model described below.

# Our model: In == Out, with DCO pull request
In choosing our model, we wanted to have high equitability, which immediately suggests
an In == Out model. But the low legal protection of pure In == Out was a concern, so 
we opted for In == Out with DCO. 

From a pure legal perspective, the entirety of open source licensing regime is predicated
on copyright law. As such, establishing copyright provenance (who owns the copyright to 
a particular piece of code) is in line with how the law handles this. As noted earlier, 
that is not the same as who authored the code. Taking this into account, led us to 
bifurcate our DCO along the lines of the contributor-is-copyright-holder vs. 
contributor-represents-copyright-holder. Instead of a ```Signed-off-by:```
commit message, we chose a ```Covered-by:``` commit message, referencing a particular
document.

The above consideration and the concern that some jurisdictions may require explicit 
agreement led us to require an explicit agreement. Furthermore, the document
referenced by the ```Covered-by:``` commit message fit well in the repository itself.
We already have lots of meta data (LICENSE, CONTRIBUTING, NOTICE, etc.) and the 
DCO's are no different. The mechanism to get anything into our repository is a pull
request, which now completes the picture: to contribute to our projects, do a one time
pull request with an appropriate DCO and reference that DCO in subsequent (code) commits.
This a "same transfer, same storage" model as described above.

# The Chain of Custody Problem
A lot of development in open source is highly collaborative. A particular piece of code
might be edited my multiple people (which sometimes, but not always, means different
copyright holders). It's also possible to start from an existing piece of OSS code
and modify it for use in another project. 

We've chosen a git-centric copyright provenance resolution. If a piece of code
has mixed copyright provenance, it must be represented as a series of commits, 
with each commit properly attributing each copyright (via a ```Covered-by:``` commit message
and potentially a by-line in the affected file).

This is very similar to the Linux Kernel ```Signed-off-by:``` semantics with two 
notable differences:

1. We care about copyright-owner, as declared in the ```Covered-by:``` DCO, not the
contributor.
2. We don't allow squashed commits with multiple ```Covered-by:``` lines.


