Title: Programmers: How Do You Partition A Collection?
Date: 2025-02-20
Tags: ai, python, java, javascript, kotlin, rust, clojure
Image: assets/images/programmers-how-do-you-partition-256.jpg
Image-Alt: An overly complex machine for dividing a collection of candy into equal amounts
Twitter-Handle: alza_bitz

![An overly complex machine for dividing a collection of candy into equal amounts](assets/images/programmers-how-do-you-partition-256.jpg)

It's a good question! Let's start by defining the problem. For our purposes a collection is defined as any number of items, and partitioning is defined as the division of said items into n groups of equal size, with the last group possibly containing fewer than n items.

Well that seems simple enough to understand. It’s a single task with only one dimension and no dependencies. I wouldn’t be surprised if a child could apply this algorithm using real objects without understanding how to code it, so it should be relatively simple for us to implement, right?

Firstly, let's see how it could be done with the three most popular languages [^1] using Stack Overflow data as a guide (captured on 14th Feb):

**Python.** Lots and lots of ways, based on the most popular post with [1.7m views and 69 answers](https://stackoverflow.com/questions/312443/how-do-i-split-a-list-into-equally-sized-chunks).

**Java.** Lots of ways, based on these popular posts with [250k views and 23 answers](https://stackoverflow.com/questions/12026885/is-there-a-common-java-utility-to-break-a-list-into-batches), [166k views and 18 answers](https://stackoverflow.com/questions/5824825/efficient-way-to-divide-a-list-into-lists-of-n-size) unless you can use Java 22. [^2]

**Javascript.** Lots and lots of ways, based on the most popular post with [1.3m views and 88 answers](https://stackoverflow.com/questions/8495687/split-array-into-chunks) unless the environment supports Baseline 2024. [^3]

In conclusion, for all these more popular languages we have 

- Many different ways, with different syntax and different apis.
- The suitability of each depends on the context (small / large, sync / async) and details of the data structure we’re working with.
- The availability of each depends on the version, of which there are many.

***

By contrast, let's look at three much less popular languages [^4] again consulting Stack Overflow:

**Kotlin.** Just a few ways, based on the most popular post with [37k views and 6 answers](https://stackoverflow.com/questions/40699007/divide-list-into-parts). Although there are 6 answers, our problem can be solved using `kotlin.collections/chunked` in the standard library from version 1.2 onwards. [^5]

**Rust.** Just a few ways, based on the most popular post with [6k views and 2 answers](https://stackoverflow.com/questions/67536734/how-to-partition-vector-of-results-in-rust). Although there are 2 answers, our problem can be solved using `trait.Iterator/array_chunks` from the standard library. [^6]

**Clojure.** I couldn’t find a specific Stack Overflow question for our case, but no matter: the top Google result takes me directly to `partition`, and from there to `partition-all`. [^7]

***

There seems to be a clear difference here. Given the same problem, these less popular languages offer a single solution in their standard libraries, which doesn’t depend nearly as much on either the context or the data structures involved.

Without getting into why this difference might exist (although see note 1 below), _we have a situation today where a large population of programmers have to either carry this complexity in their heads, or disrupt their flow to look it up, and then make a suitable choice, just to do such a simple thing?_

This might help us to understand why programmers are now using AI coding assistants to reduce context switching and work more efficiently on the actual problem they’re trying to solve.

It concerns me that we are building an ever-increasing number of more complex solutions in this way. Further, these coding assistants are only feasible due to the large data sets of questions and answers that have grown from the popularity (and shortcomings) of these languages.

**Wouldn't it be better if these simple things were made easy, to have the solutions at hand, without the absurdity of reaching for AI to help solve relatively simple programming problems?**

I think it's possible for us as programmers to do what’s asked of us, and even do it with less disruption and more efficiency, but also without “feeding the beast”. We as programmers can make a difference through our choices!

The alternative is surely a future where more and more output from these coding assistants ends up feeding the models used by those same assistants to serve these types of programming questions, and repeat. What could possibly go wrong? All this just to solve some simple problems..

**I think this is an opportunity to reflect on what we are doing, what we are using and where we are going.**

Something to ponder next time you’re trying to do a simple thing and wondering why it’s anything but!

***

### Credits.

[Igor Garcia](https://github.com/iggar) for your feedback and advice: thank you 🙏

### Notes.

**1.** A hypothesis for this difference, as to why the most popular languages don't provide  something that is independent of context or data structures, is due to incidental complexity resulting from their age and the prioritisation of backwards compatibility. The less popular languages I picked for this article are all much younger, as such they can learn from the past and adopt more recent academic research, in particular concerning data structures and the algorithms that operate on them. 

**2.** Other than the Much of this discussion isn't really new, it's just another manifestation of what happens when programmer convenience and replaceability are prioritised above all other concerns, as described by Rich Hickey in his 2011 presentation [Simple Made Easy](https://youtu.be/LKtk3HCgTa8?t=546&si=v4mc0CTZOFGA87ay).

**3.** I’m not too familiar with Rust or Kotlin so if you think my analysis is incorrect, please let me know.

**4.** Yes, I did use an LLM-based generator for the image in the header, but I’m fine with that (apart from the fact that it did not let me give any attribution or reward to the creators of the source images used by the model).

***

[^1]: [https://spectrum.ieee.org/top-programming-languages-2024](https://spectrum.ieee.org/top-programming-languages-2024)
[^2]: [https://openjdk.org/jeps/461](https://openjdk.org/jeps/461)
[^3]: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/groupBy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/groupBy)
[^4]: [https://spectrum.ieee.org/top-programming-languages-2024](https://spectrum.ieee.org/top-programming-languages-2024)
[^5]: [https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.collections/chunked.html](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.collections/chunked.html)
[^6]: [https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.array_chunks](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.array_chunks)
[^7]: [https://clojuredocs.org/clojure.core/partition-all](https://clojuredocs.org/clojure.core/partition-all)