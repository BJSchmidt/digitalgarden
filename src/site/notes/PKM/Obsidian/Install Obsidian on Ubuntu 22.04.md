---
{"dg-publish":true,"permalink":"/pkm/obsidian/install-obsidian-on-ubuntu-22-04/"}
---


When trying to install the Obsidian snap package on Ubuntu when downloaded direct from https://obsidian.md/download the follow error results:

``` bash
sudo snap install obsidian_0.7.3_amd64.snap 
error: cannot find signatures with metadata for snap 
    "obsidian_0.7.3_amd64.snap"
```

You need to add the --dangerous flag, because the snap package is not shipped with a `.assert` file.

https://snapcraft.io/docs/assertions

```
sudo snap install --dangerous obsidian_0.7.3_amd64.snap
```

https://forum.obsidian.md/t/how-to-install-obsidian-snap-on-ubuntu/2515
