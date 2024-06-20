---
title: Second contribuition to Kworkflow
---

The second issue that we decided to contribute to was [`issue #1097`](https://github.com/kworkflow/kworkflow/issues/1097). The idea was to show the current user resolution and refresh rate when running the command `kw drm --modes`

Since we already worked with this subsystem, it was pretty straightforward what we had to do. The biggest issue with this requested feature is that Siqueira sugested we parsed the file `/sys/kernel/debug/dri/0/state` to get these infos, but we need root to access these files. 

We implemented a version that needed sudo and the necessary tests, but we didn't know if the PR would be approved, since the root part was a really big problem.

As we expected, Siqueira didn't like it, but we couldn't think ourselves of a better way. Currently we are awaiting Siqueira's response toward this question. The best solution we can think of is to ask the user to write the sudo password after running the command, as today the used needs to use sudo when running the command (if he does that, the command fail since it can't read the kernel file).