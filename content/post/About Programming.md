+++
title = "About Programming"
author = ["Markus Sagen"]
date = 2021-05-09
lastmod = 2021-05-11T16:15:19+02:00
draft = false
tags = ["Philosophy", "Programming"]
+++

Harping on any one programming paradime is counter productive. Object-Oriented
Programming may be the most popular programming style for a wide set of
programming languages - I think it's safe to say that most newer languages, such
as Go, Rust etc, are moving away from that approach. I think languages should be
pragmatic and solution focused and not enforce a programmatic ideology for how
you should think about and structure your code. However, I do enforce
standardization and global standards for formatting for readability and structure. And for me, it mostly comes down to the core essence of what coding to me is about:

1.  Solving you problem
2.  Expressing your intent with your solution
3.  Making it readable and with clear intent.
4.  Isolation of concerns
5.  Solving it well

Your code will be read about 80/90% of the time, and writing it about 10/20% of the time. having you code read well and being subject to change is therefore essential. No one project starts out with a clear instruction and goal in mind. Tasks, aims and descriptions change and evolve over time as you or your customers get a better understanding of what it is you truly want and can realistically do.

-   Martin Fowler and Kent Beck's TTD (not unit tests)
-   Data-Oriented Programming
-   Leave the code in the same state as your kitchen - Clean
-   Do not take time out to refactor your code. Always do it as you work!

```python
class Graph(object):
    """A graph object."""
    def __init__(self, edges, vertices):
        self.edges = edges
        self.vertices = vertices
        self.connections = None
        self.printing = print(f"Logging {edges}")
        # Some comment
        list = [1, 2, 3]
        print(list[0])
        print("sadsdasd as das".format(self.edges))
```
