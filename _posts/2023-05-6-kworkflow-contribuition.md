---
title: First contribuition to Kworkflow
---

The issue that we decided to contribute to was [`issue #1094`](https://github.com/kworkflow/kworkflow/issues/1094). The idea was to permanently enable or disable GUI options on the DRM subsystem.

First of all, we understood the code from the `drm`  subsystem, which was not that challenging. The hardest part was understanding where the hashmap of configurations used in some functions was coming from. After some research, we found out that this hashmap was defined using the kworkflow.config file. This allows a user to override some default configurations, such as the standard enable GUI command.

After that, we made some minor modifications, including adding a flag to the kw command, obtaining the value for `gui-[on/off]-after-reboot`, and executing the command specified in the issue (or using the one specified by the user).