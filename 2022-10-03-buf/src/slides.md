---
hideInToc: true
download: 'https://github.com/kevinmichaelchen/presentations/raw/main/2022-10-03-buf/buf.pdf'
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
  ## Buf

  An easy choice
# persist drawings in exports and build
drawings:
  persist: false
---

# I ❤️ Buf

An easy choice

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/kevinmichaelchen/presentations/tree/main/2022-10-03-buf" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
  <a href="https://github.com/kevinmichaelchen/presentations/raw/main/2022-10-03-buf/buf.pdf" target="_blank" alt="GitHub"
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

# What is Buf?

#### Buf's tagline is:

##### "Building a better way to work with Protocol Buffers"


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

# What is a Protocol Buffer?

### Protocol buffers (protobufs) are Google's 

- language-neutral,
- platform-neutral,
- extensible mechanism

for **serializing structured data**.

- Think XML, but smaller, faster, and simpler.
- You **define** how you want your data to be structured **once**, then you can use special **generated source code** to **easily write** and read your structured data to and from a variety of data streams and using a **variety of languages**. 

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

# The world in 2019

---

# 2019 - protoc is hard

- [protoc](https://grpc.io/docs/protoc-installation/) is the Protobuf compilation tool.

```bash
$ brew install protobuf
$ protoc --version  # Ensure compiler version is 3+
$ protoc -I=$SRC_DIR --go_out=$DST_DIR $SRC_DIR/addressbook.proto
```

<v-click>

- It looks easy to work with.

</v-click>

<v-click>

- But is it?
  - Lots of flags: unclear what they do; easy to make mistakes
  - Lots of [plugins](https://github.com/protocolbuffers/protobuf/blob/main/docs/third_party.md): steep learning curve
  - What about more complex directory structures?
  - Bash scripts would start to accumulate
  - It soon becomes arcane

</v-click>

---

# 2019 - no good way of sharing

- There is no registry for protobufs in 2019.
  - If Service A and Service B want to use a common protobuf...
  - They have to manually copy/paste and maintain 2 separate versions. 👎
  - Imagine trying to code in JS/TS without NPM, or in Golang without Go modules. 🤯

<v-click>

- Stub distribution
  - Once you auto-generate code from protobufs, how do you distribute/share those stubs?
  - Do you centralize all your protos in a monorepo?
  - Do you have all your clients/microservices using `protoc`?
  - Do you have to worry about publishing to package registries (Maven/Gradle, NPM, Go modules, etc)?

</v-click>

---

# 2019 - other tooling is missing

- no linter
- no formatter
- no build-time compilation checkers
- no breaking-change detection
  - outages abound
- no Postman-esque tool
- not debuggable in the browser

---
layout: center
---

# 2020 - Enter [Buf](https://buf.build/)

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

# Buf CLI

- Buf's [CLI](https://buf.build/product/cli/) takes care of compiling.
- Just run `buf generate`.
- No more fiddling with protoc.

---

# Problem solved: Sharing

- The [Buf Schema Registry](https://buf.build/product/bsr/) (BSR) is a powerful tool.
  - No more copy/pasting protobufs. We can now pull dependencies.
  - We can also generate stubs [remotely](https://buf.build/product/bsr/#remote-library-generation).
  - When you push to the BSR, you can immediately download private auto-generated stubs for Go or Typescript.

```bash
$ go get go.buf.build/grpc/go/orgname/licenseapis
```

---

# Problem solved: Code Quality

- We have [linting](https://docs.buf.build/tour/lint-your-api), [formatting](https://docs.buf.build/format/usage), and [breaking change detection](https://docs.buf.build/tour/detect-breaking-changes).
- [Auto-generated docs](https://buf.build/product/bsr#generated-api-documentation) via BSR.
- We have a Postman-esque tool via [Buf Studio](https://studio.buf.build/bufbuild/eliza/buf.connect.demo.eliza.v1.ElizaService/Say?target=https%3A%2F%2Fdemo.connect.build&demo=true).
- We have a much better in-the-browser dev experience thanks to [Connect](https://connect.build/).

---
hideInToc: true
layout: center
class: text-center
---

# <uim-rocket class="text-3xl"/> finito 
