---
layout: post
title: "Double-take"
date: 2017-05-21 T19:00:00Z
---

Here at Makers, there's an incredible hunger to learn. Luckily there's a huge amount of reading material to satisfy even the most ravenous student. To help parse all of that, @codey_mccodeface  set up a Reader Dojo to share the load.

After a challenging week building an Oystercard network in Ruby, where I struggled to isolate tests, I wanted to consolidate some of the material on Test Doubles and share that in the Dojo.

_Caveat : There are way better resources than this blog on Doubles, Stubs and Mocking, check out [this page from xUnitPatterns](http://xunitpatterns.com/Test%20Double.html) immediately if you want detail_

So starting from (near) the beginning; with TDD, the idea that each object should have only one responsibility (Single Responsibility Principle) extends beyond the program; in fact it should also apply to your tests. Thinking more widely about the principle, if each object only does one thing, it should only be tested for that one thing. By encapsulating one object within the test, it shouldn't matter whether any dependants or parents fail, we want the subject under test (SUT) to be... well... the only thing subject to the test.

So how do we spoof a test to think that any other related objects (let's call them 'Collaborators') are performing as expected? The answer lies in [Doubles](http://xunitpatterns.com/Test%20Double.html).

A Double is a fake object, a dummy. They are passed around but not used in their own right and usually just used to replace some parameters. I'm not going to go into how they are implemented but they looks like this:

``` let(:fake_collaborator) { double(:fake_collaborator_identifier) } ```

That's neat, but not very useful on their own. If we're trying to prevent issues within the doubled object impacting the SUT. For that we need Stubs.

```obj.stub(:message) { 'this is the value to return' }```

``` allow(subject_under_test).to receive(:fake_collaborator)```

Stubs (such as 'allow' or 'receive') add functionality (methods) to the double in a way that we can control. They give staged responses to calls made during the test. A version of

Spies are a version of Stubs that record some information about what happened during the test and can therefore 'let you know' if something happened or didn't happen, changing ```.to receive``` to ```.have_received```. This adaptability allows us to test behaviour of the SUT, rather than just the state (remember each object only has one responsibility _to do something_).

When we start talking about testing behaviour rather than state, we start aligning to the Mockist or London School of TDD and growing TDD into Behaviour Driven Development (BDD).

<!-- "with(hash_including(:key => value))" - Allows to search through the hash and if it has this key/value pair return true, regardless of what else is in the hash_including -->

"Only talk to your immediate friends."

##### Further reading #####
**Mocks** are primed with the calls they are to receive and can throw an exception if they receive a call they don't expect.
They add an expectation on to the end of a stub like this:
```(..stub..).and_return(what_doubled_collaborator_should_return)```

There's a great resource listing the difference between Stubs and Mocks [here](https://martinfowler.com/articles/mocksArentStubs.html)

**The Law of Demeter** comes up a lot. In essence it says that you can only interact with your immediate friends. I have hit roadblocks throughout the week by trying to test a call on a call on my SUT... It makes life seriously confusing so ["do like Demeter"](http://wiki.c2.com/?LawOfDemeter) and keep your friends close.
