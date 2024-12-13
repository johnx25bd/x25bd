---
title: Retrospective — Deep Learning System Design
date: "2024-12-13T12:00:00.000Z"
template: "post"
draft: false
slug: "/posts/retrospective-deep-learning-system-design"
socialImage: "./media/delta.jpg"
category: "AI"
tags:
    - AI
description: "Reflections on MLX's Deep Learning System Design coding immersive."
---

## The mind’s limit

Earlier this year, I read [The Age of AI](https://www.hachettebookgroup.com/titles/henry-a-kissinger/the-age-of-ai/9780316273800/), by Henry Kissinger, Eric Schmidt and Daniel Huttenlocher. They argue that in human history there have been two ways of knowing — faith and reason — and that artificial intelligence represents the third way of knowing. 

<blockquote>
... we are entering a new epoch in which the reasoning human mind is yielding its pride of place as the sole discoverer, knower and cataloger of the world's phenomena.
</blockquote>
<center><strong>Chapter 1, The Age of AI</strong></center>


While I see AI more as an advanced form of reason, with more empirical evidence available for consideration, than an entirely new way of knowing, splitting hairs is unhelpful. Their insight — that AI forces us to confront the question of whether there are forms of reason inaccessible to the human mind — is both fascinating and important.

I’ve worked with or adjacent to ML for many years, but I dedicated the past four years (i.e. 100 AI years) of my career to another emerging digital technology domain that has, in my view, a comparable potential to reshape how civilization works. Over time, though, I’ve come to view “Web3” as a social innovation, rather than a technological one. Web3 systems — especially smart contracts —  don't offer any new functionality. But they do shift the way we form digitally-intermediated trust relationships in subtle-yet-profound ways. (More on this in a future post.) 

On the other hand, every month AI systems present astounding advancements in what we thought computers were capable of, and even skeptical outlooks concede that major leaps forward in the capabilities of AI systems are expected in the coming years.

## Learning how to learn

So, to get up to speed, over the last eight weeks, I participated in an immersive coding program — **Deep Learning System Design** with the [Machine Learning Institute](https://ml.institute/) (MLX) in London. MLX offers a hands-on training experience aimed at experienced software engineers designed to bridge theory and real-world application. Rather than focusing solely on lecture-based instruction, this bootcamp introduced new concepts through peer learning-driven, practical, end-to-end projects. From working with word embeddings for language tasks to experimenting with transformer architectures, every module emphasized coding, iteration, exploration and deployment.

During this intensive period, we moved through a series of time-constrained practical challenges. Some weeks focused on structuring neural networks for language understanding, while others took us into the realm of semantic search or image captioning with transformers. Each project was grounded in reproducible MLOps workflows, modern tooling for experiment tracking, and scalable deployment architectures. By the end, I had touched on all parts of the machine learning pipeline — from data ingestion and preprocessing to model deployment on containerized platforms.

Besides the theoretical fundamentals of modern deep learning systems, the most valuable lesson I took away was understanding how modular design and robust, highly organized engineering practices fundamentally shape the success of deep learning projects. Without systematic, tidy coding habits, implementing (for example) a transformer from scratch in a few days is very tricky — I saw first-hand how a well-structured codebase and automated tooling can turn complicated research code into something that’s maintainable, scalable, and ready for collaboration.

### No cutting corners

Throughout the program, one of my most formative struggles wasn’t just solving a particular bug or tuning a finicky hyperparameter — it was grappling with the underlying complexity of deep learning architectures. Rather than relying immediately on high-level frameworks or pre-trained foundation models, we spent time building seminal model components line by line. This sometimes felt slow and error-prone, especially when I knew I could achieve a “quick fix” by turning to the abundant open-source code and PyTorch utilities out there. Yet, this deliberate choice to implement key innovations from scratch yielded understanding, rather than imitation.

I’ve come to realize that, realistically, I’m not going to compete with the cutting-edge models being released from the large AI labs — nor do I need to. My future work lies in applied AI products — especially those leveraging geospatial data. This will involve rapid prototyping that uses API-based inference and fine-tuning existing large models to serve specific tasks or datasets. Even if most of my day-to-day work involves orchestrating pre-trained models rather than painstakingly crafting each transformer layer from scratch, the depth of understanding I gained from getting into the details is invaluable. Because I’ve worked directly with these architectures at a relatively low level, I’m far better equipped now to use relevant pieces of larger models, interpret model outputs, identify bottlenecks, and interact with foundation models in a much more insightful, precise and confident way.

### Gaps + Critiques

While the program offered a strong technical foundation, there were areas I believe merited more attention. In particular, the ethical dimensions of deep learning systems went largely unexplored. I understand the program’s emphasis on hands-on, rapid building, and loved that we dove straight in. Still, I see the (unsaid at MLX) belief that “we don’t have time to talk about the why, how and if we even should” all too often. I am concerned that giving deep consideration to the systems we’re building seems to be seen as a competitive disadvantage — a waste of time — rather than the moral responsibility we hold as system designers.

> [AI] is a human creation, reflecting human-designed processes on human-created machines.

<center><strong>Chapter 7, The Age of AI</strong></center>

Thanks in no small part to MLX, I’m one of the humans who can now help create this technology. Incorporating more opportunities for critical reflection into the curriculum wouldn’t have diminished the technical rigor — it would have enriched it, ensuring that as we shape these technologies, we remain mindful of the human context they serve.

## Building

I’ve included links to each (open source!) Github repo below, so instead of describing each week’s project in isolation, here are some broad themes that emerged across the work:

- **Semantic Understanding and Representation:** Early on, I noticed a pattern, that AI systems often “embed” things understandable to humans — like words, images, etc — into a mathematical space by representing them as numerical “embeddings”, “encodings”, or “representations”. This pattern emerged in the first weeks — early projects introduced me to techniques for “embedding” words in a space where they can be numerically related to other words. This laid the groundwork for downstream tasks, like implementing two-tower search architectures for semantic retrieval or species classification from audio encodings.
- **Scalable Infrastructure and MLOps:** Building search engines, classification and captioning systems wasn’t just about training a model; it was also about deploying it in a consistent, reproducible environment. I learned to containerize services, orchestrate multiple microservices with Docker Compose, and monitor experiments with tools like Weights & Biases. In the third week, my team built a template container architecture for ML applications including a front end server, a FastAPI back end, a PostgreSQL instance for data storage / logging, and more — work I’ve already reused multiple times.
- **Transformer Architectures & Multi-Modal Fusion:** Later projects dove into the complexities of transformer-based models, sometimes implemented from scratch. The idea that vision and language can be integrated in a single deep learning pipeline opened my eyes to what’s possible with attention mechanisms and unified architectures. Working with MNIST images and generating captions, or using the OpenAI Whisper encoder for birdsong classification, demonstrated that the same underlying principles of representation learning can transcend modalities and tasks.

Each of these efforts represented a step in my learning, showing me not just how to build a model, but how to structure systems that can adapt to new data, scale as complexity grows, and provide meaningful outputs in a production setting.

### Projects

- **Word Embeddings:** [johnx25bd/mlx-word-embeddings](https://github.com/johnx25bd/mlx-word-embeddings)
- **Two Tower Search:** [johnx25bd/mlx-two-tower-search](https://github.com/johnx25bd/mlx-two-tower-search)
- **Deploying search:** [johnx25bd/mlx-deploy-search](https://github.com/johnx25bd/mlx-deploy-search)
- **Transformers:** [johnx25bd/mlx-transformers](https://github.com/johnx25bd/mlx-transformers)
- **Image Captioning with transformers:** [johnx25bd/mlx-caption-deployment](https://github.com/johnx25bd/mlx-caption-deployment)
- **Birdsong Classification:** [johnx25bd/mlx-birdsong](https://github.com/johnx25bd/mlx-birdsong)
- **Landline:** a natural language interface for geospatial databases — [johnx25bd/landline](https://github.com/johnx25bd/landline)

---

## Looking Ahead

This eight-week journey has clarified my next moves. I’ll be applying these deep learning foundations to my long-standing love affair with geospatial data technologies (news on this front is pending …), among other things — as usual, stay tuned.

I’m eager to collaborate on projects that combine strong engineering fundamentals with a commitment to making positive societal or environmental impact. If you’re working on something that resonates with these themes, reach out on [Bluesky](https://bsky.app/profile/johnx25bd.bsky.social), [Twitter](https://x.com/johnx25bd) or [LinkedIn](https://www.linkedin.com/in/johnx25bd). Let’s explore ways we can leverage deep learning for meaningful work that respects human dignity and fosters planetary stewardship.