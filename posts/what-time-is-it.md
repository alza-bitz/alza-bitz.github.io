Title: What Time Is It? 
Date: 2025-05-28
Tags: data, streaming, flink, kafka, spark, storm
Twitter-Handle: alza_bitz

### Understanding the complexity of data streaming frameworks.

In a computer program, when values change over time we call this **state**. This is why we have two different words available to us for differentiating the context: the specific use of “state” instead of “value” signifies to the reader that we are intentionally composing two things, namely **value** and **time**.

Each of those concepts are simpler to reason about on their own, but when put together they require much more care. When you hear people saying “state is inherently complex”, this is what they are referring to. This is especially relevant when we are learning about **data streaming frameworks** as they need to consider state in many areas, and at scale: windowed aggregations, joins and other stateful operations, not to mention horizontal scaling, memory management through watermarks and checkpoints, fault tolerance and more.

So how best to understand the state management of these frameworks? Let’s take a look at what some of the most popular options provide to educate and inform users in this regard:

| Framework                                                                                                                                         | [Flink](https://flink.apache.org/) | [Kafka Streams](https://kafka.apache.org/documentation/streams/) | [Spark Structured Streaming](https://spark.apache.org/streaming/) | [Storm](https://storm.apache.org/) |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- | ---------------------------------------------------------------- | ----------------------------------------------------------------- | ---------------------------------- |
| Word count of reference docs                                                                                                                      | 20,042                             | 45,492                                                           | 19,908                                                            | 28,682                             |
| Informing users on stateful operations:<br>t = written text<br>d = diagrams & charts<br>a = animations<br>u = unit test facility<br>s = simulator | t,d,u,s [^1]                           | t,d,u                                                            | t,d,u                                                             | t,d,u                              |
| Execution plan checked against documented capabilities before running it?                                                                         | Yes [^2]                                | No [^3]                                                              | Yes [^4]                                                              | Yes [^5]                               |
| If a simulator is available, where does it run?<br>1 = local<br>2 = browser + server / cloud<br>3 = browser only                                  | N/A                                | N/A                                                              | N/A                                                               | N/A                                |

Based on the above, we can see that despite their level of complexity these frameworks are mostly limited to written documentation as the primary means to educate and inform users about their stateful operations. Whilst they all provide unit test facilities, such tools are intended to test your usage or composition of these operations rather than understanding the provided operations themselves. One could also argue that unit testing is targeting a later phase of your project than “educate and inform”. Finally we can see they are somewhat limited in any checks of their execution plans, and as a result things can slip through the cracks.

With that in mind, consider again that stateful data streaming problems necessarily involve the consideration of time, and as such they are fundamentally a **dynamic** concern. By contrast, written documentation is of course only **static** and for that reason I will submit that it is **inefficient and inadequate for the intended purpose**.

Indeed, I was affected by this myself in February this year when I [ran into trouble with one of these frameworks](https://stackoverflow.com/questions/79476798/spark-structured-streaming-empty-result-for-a-stream-stream-inner-join-to-compu). I still don't know if the problem I encountered is due to a misunderstanding of the (20,000 word) documentation or a [bug](https://issues.apache.org/jira/browse/SPARK-51399).

***

So what’s the solution? Well, consider that we learn best by a combination [of](https://practera.com/what-is-the-experiential-learning-theory-of-david-kolb) [reading](https://citl.indiana.edu/teaching-resources/evidence-based/active-learning.html) [and](https://www.psychologymadeeasy.in/posts/levels-of-processing-craik-and-lockhart) [doing](https://en.wikipedia.org/wiki/Generation_effect) rather than by reading alone. The “doing” is something that happens in real time, and one way to achieve this is by **simulation**.

In our case, I will define a simulation thus:

_A means to observe the effects of a stateful operation, where for the same input as given to the production equivalent, the simulation will give the same output._

Given the stated purpose of a simulator in our case is to educate and inform, I will also add to the definition that it must require zero installation or setup. Further, to reduce costs and complexity it should also require minimal resources and ideally be fully serverless or standalone in operation. Finally, since the goal is to represent stateful operations, it should be capable of representing those in a visual dynamic by using animated forms for example.

_I think there’s an opportunity for these frameworks (or new ones) to provide **visual simulators** as the primary means of reasoning for their stateful operations, and also as a complement to their existing documentation._

So with that out of the way, if we could build such a simulator what would it look like, how would it work and how could it be built? Here’s a motivational blueprint!

1. Make the simulator available in a web browser.
1. Write the core functions for the streaming solution and its stateful operations in a hosted language that compiles to code that can run in a browser. Then the same code can be used for both a production implementation and the browser-based simulation.
1. Represent unbounded inputs using generators over lazy sequences.
1. Define the execution plan specification and plan validation rules as data. Then, both the code that checks plans against the rules and any written reference guide can parse this same data, avoiding the possibility of inconsistencies.
1. Within the simulator, represent stateful operations as declarative example-based or property-based BDD style given-when-then constructs, with an animated accumulation of results over time.

In conclusion, I hope you can appreciate the benefits that simulations would bring in this space, and I also hope to have suitably motivated other people in the community to take the baton!

***

### Credits.

[Igor Garcia](https://www.linkedin.com/in/garciaigor) for your feedback and advice: thank you 🙏

***

[^1]: Flink provides an [operations playground](https://nightlies.apache.org/flink/flink-docs-release-2.0/docs/try-flink/flink-operations-playground) but it doesn’t specifically cover stateful operations. There’s also a worked example based on [fraud detection](https://nightlies.apache.org/flink/flink-docs-release-2.0/docs/try-flink/datastream), but the explanations are 100% written.
[^2]: Flink performs semantic checks for jobs defined using the Table API and SQL. However, the pre-execution validation is not exhaustive, and certain subtle errors or issues might only manifest as unexpected behavior or silent failures during runtime.
[^3]: Kafka Streams doesn’t have a distinct pre-execution validation phase in the traditional sense. Instead it relies on a combination of static type checking and the [TopologyTestDriver](https://www.confluent.io/blog/test-kafka-streams-with-topologytestdriver/) as part of a unit testing strategy.
[^4]: Spark Structured Streaming has a multi-layered validation process to ensure correctness and feasibility of computations before their execution. The [UnsupportedOperationChecker](https://books.japila.pl/spark-structured-streaming-internals/UnsupportedOperationChecker) enforces streaming-specific rules during the logical planning stage.
[^5]: Apache Storm's pre-execution topology checks focus on structural and configuration validity, and exceptions are thrown to indicate structural problems, configuration errors and authorization failures. Although it provides tools for programmatically defining and inspecting topology structure and configuration, a dedicated validation API against documented capabilities is absent.