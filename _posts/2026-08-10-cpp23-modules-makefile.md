---
layout: post
title: handling c++23 module dependency evaluation order without cmake
---

the standard tcg stack is an absolute mess of legacy c idioms, raw pointers, and manual garbage collection. when writing `tpm23`, i wanted to isolate translation units cleanly using native c++23 module boundaries (`.core`, `.nv`, `.policy`).

however, compiler support for modules in 2026 is still highly volatile. if your translation units compile out of order, the build breaks immediately under gcc 14+. 

### the solution: deterministic dependency mapping
instead of pulling in massive build systems like cmake, i wrote a raw, linear-evaluation makefile that forces exact module interface tracking. here is how the dependency topology looks...
