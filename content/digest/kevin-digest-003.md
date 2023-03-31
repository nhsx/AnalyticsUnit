---
layout: base
title: Kevin’s Biweekly Tech Digest - No.003
permalink: kevin_digest_003.html
---

**My conscience**: Are you going to address the elephant in the room?

**Me**: Huh?

**My conscience**: Still calling it a biweekly digest then?

**Me**: Yep!

**My conscience**: You have been here for much longer than two months.

**Me**: Yep!

**My conscience**: So, I guess, biweekly is a stretch goal then...?

**Me**: Sshhh! I'm trying to write this digest.

**My conscience**: Write two, I'll put on a brew.


## Best practice

In best practice, this week we discuss the monolithic repository (monorepo)...Splitting the room has never been so easy. Code repositories are where we store and track revisions to our code ~~to train our AI replacements~~, for version control and management of development. A monorepo is a single repository for the version control of several interrelated projects/libraries versus a poly/multi repo, where each codebase is tracked separately in multiple repositories. Each codebase in the monorepo, may or may not be written in different programming languages. For some, even the idea of such a flagrant disregard for separation of concerns triggers a gag reflex. For others, the fact that Google is often cited as using a monorepo is the only seal of approval they need.

Mono from the greek "monos" meaning "alone" (tips hat to Google search "etymology of mono"). This prefix can possess a negative or ominous connotation. Mono-diet (bad), monopolies (bad...depending on who you ask), monoculture in agriculture (bad), monolithic codebase (not necessarily bad, but have you heard of our lord and saviour the microservice architecture). Most, if not all, of the cited examples have good reasons for their seat on the naughty step. But why has the monorepo been met with a mixed response?

In many cases using a single repo per project is a sensible default. A monorepo in comparison seems contrary to received wisdom. How we split a project and manage the codebase is dependent on many factors including, but not limited to, our process (agile, waterfall, etc.), organisation (team structure, products) and product complexity (product architecture). However, there are times when you may wish to consider a monorepo. 

A monorepo is worth considering when:

1. The codebase is significantly large enough as to have several large teams of developer 
2. Building and deploying the entire system is complicated.
3. The main project has supporting services, libraries or bindings written in several different languages and refactoring is difficult. 


Pitfalls to consider when pursuing a monorepo:

1. Specialised tooling required to manage the workflow.
2. A large monorepos can be a burden on your IDE
3. The possibility of tightly coupled code.

As always, there is the option to mix and match mono and poly repos when managing the source version control of multiple projects. 

## Technology of the week

So you want to monorepo all the things. May I introduce you to [Bazel](https://bazel.build), [Turborepo](https://turbo.build) and [NX](). We will briefly cover Bazel in this section. However, please explore the alternatives.

Bazel allows you to manage the repo using configuration files and a command line tool. A project managed with Bazel can look as below:


```
.
├── LICENSE
├── README.md
├── WORKSPACE.bazel
├── Project1
│   ├── BUILD.bazel
│   ├── Dockerfile
│   ├── LICENSE
│   ├── README.md
│   ├── build
│   ├── cmd
│   ├── go.mod
│   ├── go.sum
│   ├── internal
│   └── pkg
├── Project2
│   ├── BUILD.bazel
│   ├── Dockerfile
│   ├── LICENSE
│   ├── MANIFEST.in
│   ├── README.md
│   ├── pyproject.toml
│   ├── setup.cfg
│   ├── setup.py
│   ├── src
│   ├── tests
│   ├── tox.ini
│   └── venv

```

**Project1** is a GoLang project and **Project2** is a Python project. The **WORKSPACE.bazel** file, found in the root directory, is used to orchestrate the build for both projects. A package is a directory hosting code and a **BUILD.bazel** file. Packages are the target of the build system.
The WORKSPACE.bazel file may contain build rules as shown below:


```bazel

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Python Rules

rules_python_version = "740825b7f74930c62f44af95c9a4c1bd428d2c53" # Latest @ 2021-06-23

http_archive(
    name = "rules_python",
    sha256 = "3474c5815da4cb003ff22811a36a11894927eda1c2e64bf2dac63e914bfdf30f",
    strip_prefix = "rules_python-{}".format(rules_python_version),
    url = "https://github.com/bazelbuild/rules_python/archive/{}.zip".format(rules_python_version),
)

# GoLang Rules

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "16e9fca53ed6bd4ff4ad76facc9b7b651a89db1689a2877d6fd7b82aa824e366",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.34.0/rules_go-v0.34.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.34.0/rules_go-v0.34.0.zip",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.18.3")

```

These rules can be executed by running:

```bash
$ time bazel build ...
```	

Output:

```
INFO: Analyzed 0 targets (1 packages loaded, 0 targets configured).
INFO: Found 0 targets...
INFO: Elapsed time: 0.547s, Critical Path: 0.02s
INFO: 1 process: 1 internal.
INFO: Build completed successfully, 1 total action
bazel build ...  0.03s user 0.03s system 9% cpu 0.603 total
```

Bazel will cache build steps and check for changes before the build processes, avoiding rebuilding and fetching dependencies when not necessary and as a result dramatically speeding up successive builds. Bazel manages deduplication, only installing a dependency found in multiple projects once. 

Detailed instruction for using Bazel can be found by following the links below:

- [Why Bazel?](https://bazel.build/about/intro)
- [Installation](https://bazel.build/install)
- [Setting up a project workspace](https://bazel.build/concepts/build-ref#workspaces)
	


## Algorithm of the week

A genetic algorithm (GA) is a search heuristic for combinatorial optimisation problems. It is a popular heuristic (I really enjoy writing GA solvers). Genetic algorithms are not universally regarded as efficient or easy to implement (**simulated annealing** *has entered the chat*). Regardless, genetic algorithms get results. So the algorithm of the week is the genetic algorithm. 

Genetic algorithms are a form of beam search while simulated annealing is an example of hill climbing. A hill climb algorithm starts at a specific point and traverses the search space in large steps searching for an optimum solution. A beam search retains a population to search for good solutions using some evaluation metric, once a good solution is found all others are disregarded and the remaining solution is the "beam". A new population is then created and the process repeats for a number of generations, in the search for a global optimum. So you could says "that's one small step for a GA and one giant leap for annealing kind..." Both are based on analogies, GAs are based on the biology of evolution and simulated annealing is based on the cooling of metals.

The basic components of the algorithm are:

- An adequate representation of the chromosome.
- A fitness evaluation and selection function.
- Operations for population management.

### The algorithm

The pseudocode below is indicative of a basic GA.

> **Algorithm 1**: Simplified Genetic Algorithm

**Input**

$$\quad$$ population size $$= n$$\\
$$\quad$$ max_generations $$=g$$\\
$$\quad$$ generation_counter $$=c$$\\
**Output**

$$\quad$$ optimum_global_solution, $$U_{g}$$

**Initialise**

$$\quad$$ population = generate_population(n)

$$\quad$$ **While(c > g)**:\\
$$\qquad$$ parent1, parent2 = select_parents(population) \\
$$\qquad$$ offspring = reproduction_operations(parent1, parent2) \\
$$\qquad$$ population = append(population, offspring) \\
$$\qquad$$ $$U_{g}$$ = evaluate(population) \\
$$\qquad$$ c++ \\
$$\quad$$ **return** $$U_{g}$$

The example pseudocode above, iterates over each generation selecting two parents at a time from the population to generate offspring. Each parent will carry a value used by the fitness function to find an optimal value. 
Some popular forms of encoding include:

- binary
- octal 
- hexadecimal 
- tree

The "reproduction_operation" can be one of several methods used to selectively recombine a portion of the parents chromosomes to create offspring and a new member of the population. To assist in finding an optimal global solution, a mutation function is used as part of the reproduction function. The mutation maintains the genetic diversity of the population.
