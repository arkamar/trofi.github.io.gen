---
title: "A small update on 'make --shuffle' mode"
date: June 21, 2022
---

# Tl;DR

GNU Make \-\-shuffle mode [entered upstream git repository](https://git.savannah.gnu.org/cgit/make.git/commit/?id=621d3196fae94e9006a7e9c5ffdaf5ec209bf832) \\o/.

For testing convenience I also tarballed the development **GNU make**
snapshot from today's [git state](https://git.savannah.gnu.org/cgit/make.git/commit/?id=84ed34ba5a32dd52600c756445f3724c9e23cf95):
<https://slyfox.uni.cx/distfiles/make/make-4.3.90.20220619.tar.lz>.

Note that **\-\-shuffle** is not enabled by default. You can enable it
by any of below methods whichever matches best your environment:

- Run **make \-\-shuffle**. For casual testing.
- Export **MAKEFLAGS=\-\-shuffle** environment variable. For day-to-day
  development or distribution-wide testing. It is also a safe value
  for **GNU make** that does not yet understand **\-\-shuffle** option.
- Apply <https://slyfox.uni.cx/distfiles/make/make-4.3.90.20220619-random-by-default.patch>
  on top of snapshot tarball. Useful for environments where there is no
  easy way to pass a parameter to **make** or to set **MAKEFLAGS**
  variable.

# minor improvements

Compared to the initial patch announced as a
[proof of concept](/posts/238-new-make-shuffle-mode.html)
there is one extra change: presence of **.NOTPARALLEL:** directive
in a **Makefile** now disables shuffling in that file.

It was done to accomodate rare projects that rely on execution order
specified in **Makefile** and don't plan to make dependencies correct
in near future. The example is **netpbm**:
<https://sourceforge.net/p/netpbm/code/HEAD/tree/trunk/GNUmakefile#l110>

# failure examples

A few new bugs were found and/or fixed:

- vim: <https://github.com/vim/vim/pull/9978>
- groff: <https://savannah.gnu.org/bugs/?62084>
- gpm: <https://github.com/telmich/gpm/pull/43>

Nothing complicated. Just a few missing dependencies.

Give it a try!