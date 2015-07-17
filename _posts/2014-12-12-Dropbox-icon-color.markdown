---
layout: post
comments: true
title: "Changing to blue Dropbox icons"
date: 2014-12-12
---

Dropbox in Linux has been upgraded to [version 3](https://www.dropboxforum.com/hc/communities/public/questions/201488805-Stable-Build-3-0-3) with a lot of changes. However, it also uses a black/while color for the indicator. These icons, for me, are very ugly. I love the blue icons of Dropbox indicator so much so I decide to switch back to the blue versions.

1. First of all, we need to download an older version of Dropbox such as [2.10.52](https://dl.dropboxusercontent.com/u/17/dropbox-lnx.x86-2.10.52.tar.gz).

2. Then extract it. After extract, go to 

```
downloadPath/.dropbox-dist/dropbox-lnx.x86-2.10.52/images/hicolor/16x16/status/
``` 

and move all of these images to override your current Dropbox icons in 

```
~/.dropbox-dist/dropbox-lnx.x86_64-3.0.3/images/hicolor/16x16/status
```

**Note**: After extracting, it is the hidden folder so press ```Ctrl-H``` to show or just use terminal to navigate.

Finally, open terminal and restart Dropbox

```
dropbox stop

dropbox start
```

Done. Dropbox icons are blue again :-)

