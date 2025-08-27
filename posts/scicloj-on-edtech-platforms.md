Title: Scicloj on EdTech Platforms: Enabling Clojure-based Data Science in the Browser
Date: 2025-08-27
Tags: clojure, scicloj, datascience, edtech
Image: assets/images/scicloj-on-edtech-platforms-256.jpg
Image-Alt: Browser window showing a live demo of my data science PoC
Twitter-Handle: alza_bitz

You may or may not be aware that the Clojure data science stack a.k.a. [Scicloj](https://scicloj.github.io/) has been gaining momentum in recent years. To give a few highlights, [dtype-next](https://cnuernber.github.io/dtype-next/index.html) / [fastmath](https://generateme.github.io/fastmath/fastmath.core.html) are comparable with [scipy](https://scipy.org/) / [numpy](https://numpy.org/) for numerical work, and [tech.ml.dataset](https://techascent.github.io/tech.ml.dataset/walkthrough.html) / [tablecloth](https://github.com/scicloj/tablecloth) are comparable with [Pandas](https://pandas.pydata.org/) for tabular data. Kira McLean's [2023 Conj presentation](https://youtu.be/MguatDl5u2Q) explains that feature parity is almost upon us, and also offers some reasoning on why data scientists are now considering Clojure as an alternative to Python or R.

However, the leading EdTech platforms don't have much support for Clojure so all the potential benefits of both the language and Scicloj are not currently accessible to those communities.

**The good news** is that I have created [a proof-of-concept for using a browser to write, load and evaluate Clojure code](https://github.com/alza-bitz/nrepl-ws-client) running on a [remote server using websockets](https://github.com/alza-bitz/nrepl-ws-server), processing the results for display using the Scicloj notebook library [clay](https://github.com/scicloj/clay).

I don't believe this combination has been achieved before. It is a significant step when you consider that Scicloj is Java/JVM-based on account of the underlying math support, there is no Javascript or ClojureScript implementation and that is likely to remain the case.

**This work opens up the possibility for Clojure-based data science on e-learning platforms** so that anyone anywhere can learn and experiment with the Scicloj stack.

Here are some examples of new e-learning content that could be unlocked..

Theory:

- Value vs state & functional programming
- Concurrent programming.

Clojure hands-on:

- Interactive programming and structural editing with the REPL
- Data processing with lazy sequences and transducers
- Data science notebooks covering stats, ML or LLM with rendered tabular data and charts.

More recently I gave an update on my progress at the [Scicloj Visual Tools #34 meetup](https://clojureverse.org/t/visual-tools-meeting-34-clojure-in-wasm-docker-nrepl-el-nrepl-ws-clay-summary-partial-recording/11452), including a live demo:

[![Watch the video](https://img.youtube.com/vi/i3x0z9mzWm0/hqdefault.jpg)](https://youtu.be/i3x0z9mzWm0?si=LfzqCQTdFFBaAGjP&t=50)

I hope you can appreciate the opportunity here. I'm happy to give a live demonstration to anyone who's interested!