---
date: 2026-05-18
source: [[WA - 03]]
tags: [software-engineering, devops, tools]
---
# Software Engineering Tools

## Overview
Analysis of the fundamental toolchain used in modern software development to manage source code, automate builds, and standardize deployment environments.

## Version Control with Git
Source code management is handled through a [[Distributed Version Control System]], with [[Git]] being the industry standard.
- **Core Function**: Manages revisions of files, allowing for branching, merging, and tracking history.
- **Key Files**:
    - `.gitignore`: Specifies intentionally untracked files to ignore.
    - `README`: Provides essential project documentation.

## Build Automation with Apache Maven
[[Apache Maven]] is used to manage the lifecycle of a Java project, from compilation to deployment.
- **Primary Goals**: Ensures coherence, reuse, simplicity, and ease of maintenance.
- **Project Object Model (POM)**: The central XML configuration file (`pom.xml`) that defines project dependencies, plugins, and build goals.
- **Capabilities**: Handles dependency management, packaging (e.g., creating `.war` files), and documentation.

## Environment Standardization with Docker
[[Containerization]] solves the "it works on my machine" problem by packaging applications into isolated, self-sufficient environments.

### Docker Core Components
- **[[Docker Engine]]**: The runtime environment that manages containers on the host.
- **[[Docker Image]]**: Immutable, read-only templates composed of layers.
- **[[Dockerfile]]**: A declarative script used to build an image.
- **[[Docker Container]]**: A runnable instance of an image.

### Data and Networking
- **[[Docker Volume]]**: Provides persistent storage outside the container's volatile filesystem.
- **[[Docker Network]]**: Enables isolated containers to communicate with each other.

### Orchestration with Docker Compose
[[Docker Compose]] simplifies the management of multi-container applications using a single YAML file.
- **Services**: Scalable components (e.g., a web server and a database).
- **Ports**: Mapping between the host and the container.
- **[[Healthcheck]]**: Verification that a service is "ready" and not just "started".
- **Dependencies**: Defined via `depends_on` to control the startup order.
