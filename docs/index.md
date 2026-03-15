# **ReproGen**

[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json)](https://github.com/copier-org/copier)
![Python](https://img.shields.io/badge/python-3.9%20%7C%203.10%20%7C%203.11-blue.svg)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/a7med7x7/chamelab-cli)](https://github.com/a7med7x7/ReproGen/releases)
[![Demo Tutorial](https://img.shields.io/badge/demo-LLM%20Experiment-purple.svg)](https://github.com/A7med7x7/ReproGen/tree/training-demo)

Chameo is a CLI tool for generating **reproducible machine-learning workflows from templates**, designed for researchers, students, and engineers working on **Chameleon Cloud**.

It scaffolds your project structure, Dockerized environment, MLflow tracking setup, and training templates, all based on your answers to a few guided prompts.

![chameo create project](./images/chameo.png)

---

## **Why Chameo?**

Reproducibility is a cornerstone of science, yet it remains a major challenge. Many experiments lack proper tracking, dependency management, and artifact sharing, making it difficult to reproduce results, even for the original authors.

Chameo bridges this gap by providing **ready-to-use templates** that integrate reproducibility into your workflows. With Chameo, you can focus on your experiments while it handles the infrastructure, and maximizing reproducibility. 

### Key Benefits:
- Simplifies adoption of MLOps practices for researchers.
- Provides templates with built-in experiment tracking, versioning, and artifact persistence.
- Enables reproducible workflows on platforms like **[Chameleon Cloud](chameleoncloud.org)**.

For a deeper dive, see **[Why Chameo](why.md)**.

---

## **Installation**

Chameo requires Python 3.9+. We recommend installing it with pipx. Installation command options:

=== "With pipx (recommended)"

    ```bash
    pipx install chameo
    ```

=== "With pip"

    ```bash
    pip install chameo
    ```

=== "With conda (coming soon!)"

    ```bash
    ```

---

## **Quickstart**

To create a project:

```sh
chameo create myproject
```