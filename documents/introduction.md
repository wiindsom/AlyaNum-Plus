---
title: Introduction
---

# Introduction

Have you ever wanted to have really, really, massively, humungously and hilariously large numbers in your Roblox game?
Well, you probably already could, except at the cost of performance.

AlyaNum, a fork of [OmegaNum](https://create.roblox.com/store/asset/11646892509/OmegaNum-Readable) by FoundForces and [Naruyoko](https://github.com/Naruyoko),
focuses on performance by rewriting OmegaNum's unoptimized code (this sounds stupid but the codebase was so unreadable no one would dare try doing it).

Well, AlyaNum is here to tell you that you don't have to suffer anymore. No longer are the days when you have thoughts in your mind that "Maybe I should probably
stop using such a slow piece of crap."

With a limit of 10^^^^^10, where ^^^^^ is heptation, go wild. Enjoy the library!

## Installation
AlyaNum is pretty easy to install and use!
To get started, download the library from any of the following options:

1. [Roblox Toolbox](https://create.roblox.com/store/asset/18985449198/AlyaNum)
2. [Wally](https://wally.run/package/evilbocchi/alyanum)
3. [npm for roblox-ts](https://www.npmjs.com/package/@antivivi/alyanum)

## Basic Usage
Example in Lua:
```lua
local AlyaNum = require(path.to.AlyaNum)

local number = AlyaNum.new(5) -- make a new object representing 5
print(number) -- 5
local toAdd = AlyaNum.new(250)
toAdd = toAdd:mul(2) -- You can choose to use the provided macro functions...
number = number + toAdd -- Or simply use metamethods
print(number) -- 505
```

Example in TypeScript:
```ts
import AlyaNum from "@antivivi/AlyaNum";

let number = new AlyaNum(5); // make a new object representing 5
print(number) // 5
let toAdd = new AlyaNum(250);
toAdd = toAdd.mul(2); // You can only use macros due to TypeScript limitations
number = number.add(toAdd)
print(number) // 505
```

