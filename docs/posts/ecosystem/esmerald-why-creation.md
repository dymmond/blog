---
date: 2023-09-02 
categories:
  - Technology
  - Ecosystem
  - Esmerald
slug: esmerald-why-did-i-create-it
authors:
  - tarsil
---

# Esmerald — Why did I create it?

<img src="https://res.cloudinary.com/dymmond/image/upload/v1673619342/esmerald/img/logo-gr_z1ot8o.png" alt="Esmerald" />

Hello everyone, my name is Tiago Silva and I’m the creator of the Python web framework, [Esmerald][esmerald].

**Official documentation**: [https://esmerald.dev][esmerald].

This article aims to explain the reasoning behind the creation of such framework and why I believe
it fits inside the Python ecosystem.

This also marks the beginning of the first official Dymmond's blog.

<!-- more -->

## Background

Before going into more details about Esmerald I find it important to give a background explanation
about who I am and how/why this actually happened.

It is very, very important to understand that I am not against any existing framework neither does Esmerald "compete" with anything here.

I'm an experienced software engineer with 12+ years of experience (by the time of the writing) and worked with a
panoply of technologies along the way with heavy focus on Python.

During my career I've used Django, Flask, Bottle, Pyramid and some other tools that helped me do my job when those were required and this was the beginning for me.

I am also an open source enthusiast and the creator of some tools being used by a lot of people out there like Django Tenants URL and Django Messages DRF, among others.

A few years ago alongside a very close friend of mine, also a software engineer, were thinking about 
the hurdles and gaps we find in some of the ecosystems out there in different technological areas and 
languages and imagining if we could help fill some of those gaps. 

There, the first iteration of what it would become Dymmond, was born.

## Dymmond

Initially, this was the codename given to our "pet project", to our idea of filling a specific gap,
in this case in the Python world.

This happened more than 5 years ago and we didn't move too much due some constraints along the way (Yes COVID,
I'm looking at you) and our lives continue.

In 2022 I was working for an amazing company in a client that itself was demanding for the type of business required.
I won't go through details here because those are not relevant but long story short, it was when the idea of bring back Dymmond started to happen.

## The challenges

During my working experience I came to realise that I was using different tools and frameworks to solve
simple problems. My frustration kicked in there. I remember thinking:

> But why do I need to go through all of this work for a simple API or a simple integration? 
> Why I can't have all in one place, like a scaffold that allows me to have all in one place but without bloating the system?

Again, Dymmond came back to my mind and that idea that I had with that friend so many years ago about the gaps was making even more sense.

And here it was when I decided to take after hours of work (a lot of extra hours after work to be more precise) and starting designing what would become Esmerald.

**Dymmond became the company behind of it.**

## Esmerald

I understand what you might be thinking now, something around these lines, probably:

> Sure, "another" framework but now we have FastAPI, why didn't you simply use it?


And this would be an extremely fair question with a simple answer. Because FastAPI although being a
fantastic Python framework and doing the job it was designed to do really well was not yet solving
the problems and the gaps I was facing and 99% of the developers I met were facing as well.

Remember that friend I mentioned before? Well, he also worked with a lot of different technologies
in the past (and even now) besides Python and the stack he usually **works is business oriented, SAP**.

This was an important point for the design and conception of Esmerald and that was due to the fact
that he mentioned some frustrations regarding the way a lot of Python projects were developed.

I remember chatting with him a lot and this came out:

> One of the biggest problems I find with Python projects and some other too but here specifically
in Python is the lack of clear guidelines or ways I could separate business logic from application logic

Again, I'm sure you might be now thinking:

> That is because your friend doesn't know Python or the principles and if he pays attention,
> there are plenty of ways of getting that one done

And again, this would be fair way of thinking as well but in reality he actually got a point.
I'm not saying we don't have ways of doing things properly,
after all Python is so versatile that saying there is **one way of doing it right** would be… wrong!

It also important to mention that friend **didn't say any of that**. What he actually meant was a
**clear guideline** when developing using a given tool and here I agree 100% with him but this is simply the developers point of view.

## Inspirations

It is also very important to mention that I love Django, Flask, FastAPI and so on and I used them when I needed to.

Esmerald came to be inspired by the great work of others and from those who paved the way
for the evolution of tech to happen and I don't think that one tool does it all.

## The beginning of a journey with Esmerald

When I was initially thinking about what I would bring to the table with Esmerald in order to simplify the development process, that was clear to me.

I needed to marry business, data and development in one where possible and provide the necessary scaffolds and tools for the engineers to feel comfortable as well as being easy to design and implement.

My initial thoughts about what Esmerald should provide out-of-the-box were:

* Clear syntax;
* Clear routing system and as versatile as possible;
* A way of designing a clear permission system;
* Integration with OpenAPI;
* Easy integration with 3rd party tools and even legacy systems when needed;
* Modularity and clear possibility for separation of concerns;
* OOP and functional principles;
* **A guideline for integration of business logic and application logic;**
* A unique clear settings system that would allow security to take place easily. This was possible thanks to the integration with Pydantic.

And a lot more that came along the way during the last few months.

In the end it was mandatory to be **Elegant**, **Modular** and **Pluggable**.

Did you read the guideline integration? Well, that friend played a crucial role in the 
development of the mindset of [Esmerald][esmerald], I even risk to say that without him, [Esmerald][esmerald] wouldn't even
exist in the way it is in the first place. Here was where the [Esmerald][esmerald] DAOs were born!

[Esmerald][esmerald] for the first time marries business with technology in a clear way and I find that beautiful.
For the first time the business won't be resilient with technology neither developers with the business requirements.

**The maintenance of a highly scalable and performant application became easy, and most importantly, became clear.**

Here Esmerald came to be and officially paving the way for other great developers to deliver what the business demands in such speeds that makes it almost unbelievable.

## The simple hello world

Although Esmerald being extremely powerful and complex internally, it was always designed to be simpler for the people using it and the way of testing its by launching the classic "Hello, World!".

Esmerald getting inspiration by the great designs out there was never meant to be complex when starting and so kept a familiar way of starting an application by not scaring people off.

### Installation

```shell
$ pip install esmerald
```

### The application

The main page of the documentation already has this example there as well.

```python
from esmerald import Esmerald, Gateway, get


@get('/')
async def hello() -> str:
  return "Hello, World!"


app = Esmerald(
    routes=[
        Gateway(handler=hello)
    ]
)
```

As you can probably see, Esmerald preserved the simplicity from its inspirations and the familiarity it is simply there.
Now, is it only this? Of course not, this is just the hello world and the documentation goes in great detail about the routing system, interceptors, integrations, permissions and lot more you can do.

Welcome to [Esmerald][esmerald] world.

## Conclusion

I understand the resilience of using Esmerald. After all like everything, there are plenty of other tools that do a great job and do it well and Esmerald is the new kid in town.

So, for that reason, I challenge you to use Esmerald, play around with it and help growing the ecosystem to get into the place where everyone can enjoy and take benefits from it.

You can contribute in any way to Esmerald. It is open source and free to be used by anyone as well as welcomes any enthusiastic developer to contribute with its own ideas and who knows, bringing more use cases onto the table.

## Last thoughts

This article was never aimed to go technical on Esmerald and I know some people are already using and enjoying Esmerald which makes me happy and with the feeling of mission accomplished.

This article was just to explain the reasons that made Esmerald possible and welcomed in the Python community without going through a whole three hour reading essay.

It is a long path to go to have people using it without thinking about "competition" or even to get contributors on board but in the same way Esmerald that was 
initially Dymmond and took time to come to be, this is also a journey to get there and not a sprint.

Looking forward to have a great community behind Esmerald as well as behind the whole Python ecosystem, after all we are here to help each other growing and getting better.
Thank you for reading this.

## External links

If you liked this article and liked the idea of Esmerald and would like to give it a try, I salute you for that and you can clap and share the article for others to enjoy too.

There is a dedicated Discord channel for Dymmond where we can debate ideas, bugs or all in between.

* **Discord**: [https://discord.gg/eMrM9sWWvu](https://discord.gg/eMrM9sWWvu)
* **Twitter**: [https://twitter.com/apiesmerald](https://twitter.com/apiesmerald)
* **Github**: [https://github.com/dymmond/esmerald](https://github.com/dymmond/esmerald)

If you like the tools built and would like to try something more:

* **Lilya**: [https://lilya.dev](https://lilya.dev). An ASGI Python toolkit.
* **Saffier**: [https://saffier.tarsild.io](https://saffier.tarsild.io). An async ORM for Python.
* **Edgy**: [https://edgy.tarsild.io](https://edgy.tarsild.io). Another async ORM for Python but built 100% on top of Pydantic.
* **Mongoz**: [https://mongoz.tarsild.io](https://mongoz.tarsild.io). An ODM with Pydantic for MongoDB with a familiar interface.
* **Asyncz**: [https://asyncz.tarsild.io](https://asyncz.tarsild.io)

[esmerald]: https://esmerald.dev