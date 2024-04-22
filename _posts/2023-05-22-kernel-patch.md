---
title: Linux Kernel: Setting up development environment
description: In this post i'll share my experience in setting up my environment to contribute to the Linux Kernel
author: cotes
date: 2022-05-21 11:33:00 +0800
categories: [Blogging, Free Software]
tags: [kernel]
pin: true
math: true
mermaid: true
---

For our first patch, we had some suggestions to follow, and i choose the one which our objective was to use the function device_for_each_child_node_scoped() to simplify error handling.

The motivation behind this patch is that some drivers iterate throught firmware nodes, and the problem is that if the loop ends early, it doesn't necessarly releases the node reference.

The device that i made my change was:

*drivers/iio/adc/mcp3564.c*


```c
@@ -998,7 +998,6 @@ static int mcp3564_parse_fw_children(struct iio_dev *indio_dev)
        struct mcp3564_state *adc = iio_priv(indio_dev);
        struct device *dev = &adc->spi->dev;
        struct iio_chan_spec *channels;
-       struct fwnode_handle *child;
        struct iio_chan_spec chanspec = mcp3564_channel_template;
        struct iio_chan_spec temp_chanspec = mcp3564_temp_channel_template;
        struct iio_chan_spec burnout_chanspec = mcp3564_burnout_channel_template;
@@ -1025,7 +1024,7 @@ static int mcp3564_parse_fw_children(struct iio_dev *indio_dev)
        if (!channels)
                return dev_err_probe(dev, -ENOMEM, "Can't allocate memory\n");

-       device_for_each_child_node(dev, child) {
+       device_for_each_child_node_scoped(dev, child) {
                node_name = fwnode_get_name(child);

                if (fwnode_property_present(child, "diff-channels")) {
@@ -1041,13 +1040,11 @@ static int mcp3564_parse_fw_children(struct iio_dev *indio_dev)
                        inputs[1] = MCP3564_AGND;
                }
                if (ret) {
-                       fwnode_handle_put(child);
                        return ret;
                }

                if (inputs[0] > MCP3564_INTERNAL_VCM ||
                    inputs[1] > MCP3564_INTERNAL_VCM) {
-                       fwnode_handle_put(child);
                        return dev_err_probe(&indio_dev->dev, -EINVAL,
                                             "Channel index > %d, for %s\n",
                                             MCP3564_INTERNAL_VCM + 1,
--
```


So, what i had to do to fix this bug was:
1. use *device_for_each_child_node_scoped()* function
2. remove all *fwnode_handle_put()*
2. remove *fwnode_handle* pointer.
