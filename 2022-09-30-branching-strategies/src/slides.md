---
hideInToc: true
download: 'https://github.com/kevinmichaelchen/presentations/raw/main/2022-09-30-branching-strategies/branching-strategies.pdf'
# try also 'default' to start with a default theme
# theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
# highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Git Branching Strategies

  Moving safely and quickly as a team
# persist drawings in exports and build
drawings:
  persist: false
---

# Git Branching Strategies

Moving safely and quickly as a team

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/kevinmichaelchen/presentations/tree/main/2022-09-30-branching-strategies" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
  <a href="https://github.com/kevinmichaelchen/presentations/raw/main/2022-09-30-branching-strategies/branching-strategies.pdf" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-download />
  </a>
</div>

---
hideInToc: true
layout: intro
---

# Kevin Chen

<div class="leading-8 opacity-80">
Software Engineer at <a target="_blank" href="https://teachingstrategies.com"><icons8-student class="opacity-50 ml-1"/> Teaching Strategies</a>.

<div class="my-2">
Formerly at
<a target="_blank" href="https://drivers.coop"><ri-roadster-line class="opacity-50"/> The Drivers Coop</a>,
<a target="_blank" href="https://care.com"><cil-baby class="opacity-50"/> Care.com</a>, and
<a target="_blank" href="https://irisvr.com"><eos-icons-virtual-reality class="opacity-50"/> IrisVR</a>.<br>
</div>

<div class="mt-2">
Fan of chess, racket sports, skiing, guitar.
</div>
</div>

<div class="my-6 grid grid-cols-[40px,1fr] w-min gap-y-4">
  <ri-github-line class="opacity-50"/>
  <div><a href="https://github.com/kevinmichaelchen" target="_blank">kevinmichaelchen</a></div>
  <ri-twitter-line class="opacity-50"/>
  <div><a href="https://twitter.com/kevinmchen" target="_blank">kevinmchen</a></div>
  <ri-mail-send-line class="opacity-50"/>
  <div><a href="mailto:kevin.chen@teachingstrategies.com" target="_blank">kevin.chen@teachingstrategies.com</a></div>
</div>

<img src="https://avatars.githubusercontent.com/u/5129994?v=4" class="rounded-full w-40 abs-tr mt-16 mr-12"/>

---
hideInToc: true
---

# Table of Content

<Toc listClass="!list-disc" maxDepth="2" />

---
layout: center
---

# What is a Git branch?

- 🖖 Branches allow developers to **diverge** from the main branch by creating
  separate branches to isolate code changes
- 👉 A branch is essentially a reference or a **pointer** to the latest commit in
  a given context; it’s not a container for commits.
- 🪶 The Git branching model is **lightweight** compared to other version control systems.
- ⛓️ Branches allow for **independent** lines of code that branch off the master branch, allowing developers to work independently before merging their changes back to the code base.

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: center
---

# What is a Git branching strategy?

Branching strategies help to

- 🧠 Enhance productivity by ensuring proper **coordination among developers**
- ⛓️ Enable **parallel development**
- 🏗️ Help organize a series of **planned, structured releases**
- 🛣️ Map a clear **path** when making changes to software through to production
- 🐛 Maintain a **bug-free** code where developers can quickly fix issues and get these changes back to production without disrupting the development workflow

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: image-right
image: https://www.flagship.io/wp-content/uploads/gitflow-branching-strategy.png
background-size: contain
---

# GitFlow

Created by Vincent Driessen:[^1]

<v-click>

There are 2 immortal branches:

</v-click>

<v-clicks>

- `master` branch is always production-ready.
- `develop` always has the latest delivered dev changes.

</v-clicks>

<v-click>

There are 3 types of supporting branches:

</v-click>

<v-clicks>

- **feature** — both branched off and merged back into `develop`; typically only exist on localhost, not in the remote.
- **hotfixes** — branched off `master` and merged back into both `developer` and `master`
- **releases** — branched off `develop` and merged back into both `developer` and `master`

</v-clicks>

<div v-click>

When `develop` basically resembles a new release, that's when the release branch
is created.

</div>

[^1]: [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/)

<style>
p {
  @apply text-sm;
}
li {
  @apply text-xs;
}
</style>

---
hideInToc: true
---

# Downsides of GitFlow

<div grid="~ cols-2 gap-4">
<div>

A note from Gitflow's creator:
<blockquote class="mt-4 leading-6 w-5/6">
Web apps are typically continuously delivered, not rolled back, and you don't 
have to support multiple versions of the software running in the wild...
</blockquote>
<blockquote class="mt-4 leading-6 w-5/6">
If your team is doing continuous delivery of software, I would suggest to adopt
a much simpler workflow (like GitHub flow) instead of trying to shoehorn git-flow
into your team...
</blockquote>
<blockquote class="mt-4 leading-6 w-5/6">
If, however, you are building software that is explicitly versioned, or if you
need to support multiple versions of your software in the wild, then git-flow
may still be as good of a fit to your team as it has been to people in the last
10 years.
</blockquote>



</div>
<div class="mb-[-100px]">

<Tweet id="1573001023064789000" scale="0.65" />

</div>
</div>

---
hideInToc: true
---

# If not GitFlow, then what?

<div grid="~ cols-2 gap-4">
<div>

<v-click>

Constant, continuous feedback is ideal.
We can't afford to wait too long to check if my changes work with yours.

</v-click>

<v-click>

Branches, by definition, are designed to isolate and hide change.
Continuous integration, by definition, is designed to expose change.

</v-click>

<v-click>

GitHub Flow[^1] (aka plain old _feature branching_) is a good alternative.

</v-click>

<v-click>

Farley encourages developers to merge directly into trunk, but that seems to
subvert the Pull Request reviewing process. PRs are also useful for squashing
commits and keeping trunk history tidy.

</v-click>

<br>
<br>

[^1]: [GitHub Flow](https://githubflow.github.io/)

</div>
<div class="mb-[-100px]">

<Tweet id="1442448180323528704" scale="0.55" />

</div>
</div>

---
layout: center
---


# What about marketing releases?

<v-click>

Long-lived branches are eschewed.

Commits are flying into main branch.

A robust testing suite inspires confidence.

</v-click>

<v-click>

But what about work done towards a marketing release with a special launch date?

What if a new feature isn't supposed to be enabled until the New Year, for example?

</v-click>

---
title: Feature flags to the rescue
layout: center
class: text-center
hideInToc: true
---

# Feature flags to the rescue

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
hideInToc: true
layout: center
class: text-center
---

# <uim-rocket class="text-3xl"/> finito 
