---
date: 2024-04-16
categories:
  - Technology
  - Ecosystem
  - Esmerald
  - Community
slug: esmerald-roadmap-approach
authors:
  - tarsil
comments: true
---

# An interesting question from the community

[Esmerald][esmerald] has been growing steadily and the community behind it is just amazing.

In the recent weeks it has been some conversations about the roadmap of [Esmerald][esmerald] and
what it would be a great idea moving forward.

!!! Note
    This is not a long article about the future of Esmerald but a simple design approach to a question
    raised by the community.

Before continuing, let us dive into the why this is happening.

<!-- more -->

## The beginning

[Esmerald][esmerald], as a lot of people know, it was initially built on top of Starlette. Like
many frameworks out there such as FastAPI, Starlette plays a pivotal role in the core of those.

With the need of having a more granular control over the core and internal API plus some extra functionalities
that we belived to be essencial to a toolkit, [Lilya][lilya] was born.

!!! Note
    It is important to understand that Starlette is a fantastic and very powerful framework and this
    article has **nothing against it** at all.

With Lilya created, Esmerald could replace its core from Starlette and completely adopt Lilya.

This also meant that core functionalities of Lilya could also be used and bring value onto the framework.

## Pydantic and MsgSpec

Esmerald natively has pinned down the support for **Pydantic** and **MsgSpec** and the reason for this
its because both are extremely powerful and widely adopted and Pydantic offers a fantastic approach
to design the OpenAPI documentation of Esmerald.

## The community

Recently it was brough to my attention by the community the need of extending Esmerald to also support
other libraries.

I do believe this is actually a great idea that would make Esmerald **future proof** and compatible
to other libraries at your choice, like **marshmallow** or **attrs**.

But how can this be done in reality?

### The approach

Esmerald operates in a clean fashion, it enforces the typing on the handler and makes sure you are
passing the right typing when calling the endpoint.

This design is done by the internal `transformers` where an internal `signature` is being created
and validated against.

Rewritting the transformers would be the go to approach to decouple from the pinned libraries and
make it agnostic to any library at choice from the developer using the framework.

But again, is this enough? Would this rewritting of the transformers do the job? Well, short answer
I would say yes but do we actually need to do all of the logic for it? No.

#### Enters Lilya

With the migration from Starlette to Lilya, Esmerald gained superpowers, that means, why is it needed
to reinvent the wheel for the transformers when [Lilya][lilya] already does it for us?

[Lilya encoders](https://www.lilya.dev/responses/#build-a-custom-encoder) are the ones to look out
for.

The logic that Esmerald actually need to be compatible with anything new actually can be achived by
registering the encoders in Lilya and delegate all the validations to them.

Lilya does a lot of the heavy lifiting for you so there is no logical reason to use what is already
there.

There are also a lot more functionalities that can be reused from the toolkit but for the purposes
of this scenario, let us just focus on the encoders.

#### How does an encoder look like

Well, as per the documentation, designing registering an encoder is in fact very simple.

```python
from typing import Any

import msgspec
from msgspec import Struct

from lilya.encoders import Encoder, register_encoder


class MsgSpecEncoder(Encoder):
    __type__ = Struct

    def serialize(self, obj: Any) -> Any:
        """
        When a `msgspec.Struct` is serialised,
        it will call this function.
        """
        return msgspec.json.decode(msgspec.json.encode(obj))


# A normal way
register_encoder(MsgSpecEncoder())

# As alternative
register_encoder(MsgSpecEncoder)
```

Now this is in fact something quite clean.

So, if moving to this approach would be ideal, how could we be sure that the current developers using
the framework would not be affected? And by affected, I mean, with the upgrade the system would not blow?

Well, if Esmerald already supports Pydantic and MsgSpec, we still need to make sure this continues so
we provide Esmerald native encoders already registered.

Something like this, but internally, of course.

```python
from __future__ import annotations

from typing import Any

import msgspec
from msgspec import Struct
from pydantic import BaseModel

from lilya.encoders import Encoder, register_encoder

class PydanticEncoder(Encoder):

    def is_type(self, value: Any) -> bool:
        return isinstance(value, BaseModel)

    def serialize(self, obj: BaseModel) -> dict[str, Any]:
        return obj.model_dump()



class MsgSpecEncoder(Encoder):
    __type__ = Struct

    def serialize(self, obj: Any) -> Any:
        return msgspec.json.decode(msgspec.json.encode(obj))


register_encoder(PydanticEncoder())
register_encoder(MsgSpecEncoder())
```

Maybe we could also provide a way of cleanly register any encoder in the application, for example:

```python
from esmerald import Esmerald


app = Esmerald(...)
app.register_encoder(...)
```

!!! Warning
    `app.register_encoder` does not currently exists in Esmerald, this was done as an example
    of an approach.


## Final thoughts

Utilising Lilya and the encoders would be a very good approach to decouple the transformers of Esmerald but
is there any other way to make it happen? I'm sure there is and the future of Esmerald looks brigher
than ever and the upcoming version 4 of Esmerald too.

It will take time to get into this place and design but one thing we know for sure is that we will
be definitely doing this and all because Esmerald is being pushed by the community.

Whatever the community decides its what is going to be added, refactored, removed...

{!> ../docs_src/shared/external_links.md !}

[esmerald]: https://esmerald.dev
[lilya]: https://lilya.dev
