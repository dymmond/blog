# Dymmond Blog

This is the official repository for the blog of Dymmond.

In the space everyone can contribute, within reason, to any article that would like to see it
publish in the blog. We have decided to make it open source because of the nature of the blog.

Dymmond uses [mkdocs-material for blogs](https://squidfunk.github.io/mkdocs-material/setup/setting-up-a-blog/#writing-your-first-post)
which makes it great for this.

## First steps

First, you will need to fork the repository to yourself and install the requirements.

### Requirements

* Python 3.8+

### Installation

Once the repository is forked you can install the requirements (we advise to use a virtual environment)
for this.

You can run:

```shell
$ make requirements
```

Or alternatively:

```shell
$ pip install -r requirements/base.txt
```

This will ensure all the necessary requirements for the blog are properly installed.

### Run the blog locally

Once everything is installed, you can simply run:

```shell
$ make serve-docs
```

Or alternatively:

```shell
$ mkdocs serve
```

## How to contribute with articles

This is the easiest part. The blog works like a normal open source contribution, meaning, you will
need to open a pull request for your article and then once its merged, the system will automatically
publish the article for you in a matter of minutes.

Why is this process like this? Well, we want to make sure all the articles are revised and without
harmful/malicious content or intent.

Publishing the articles is free but we need to ensure the integrity of the blog.

## Which content is allowed to be published

Well, this neat part, you can write about anything you want. From Esmerald, FastAPI, Lilya... To even any
other subject that you would like to see it there. We have no restrictions at all.

## How to write an article

Once the the local environment is up and running you can access your localhost:

```shell
http://localhost:8000
```

**The articles must be placed inside the `docs/posts`**, always.

The `docs/posts` already have some pre-defined folders that can ease your choice of where the article
should be placed but if you see that maybe a new one should be created that is closer to what you
are trying to achieve, by all means, create it but bare in mind that should be the last option as
we believe the existing folders are generic enough.

You can also place a folder inside existing folders as the blog will automatically detect them and
display it.

### Add yourself as an author

If you are new into Dymmond's blog, you would want to add yourself as an author of the article, right?

Well, for that to happen you will need to update the `docs/.authors.yml` to make sure you github
handler is properly set and you can use it in your articles.

**Example**

```yaml
authors:
  spiderman:
    name: Peter Parker
    description: Author
    avatar: https://github.com/spiderman.png
```

Then in your article, on the top of the `.md` file.

```yaml
---
date: 2024-04-01 
categories:
  - Technology
  - Opinion
slug: the-article-slug
authors:
  - spiderman
---
```

You can check the examples of the already written articles in case you have any questions.

### The categories

These are the classifiers of the article, basically where you can filter them out when selecting
a specific category.

**Make sure you classify it approperly or the PR will be rejected.**

## Final notes

We hope you have fun in doing this and any improvement/contribution is more than welcomed.
