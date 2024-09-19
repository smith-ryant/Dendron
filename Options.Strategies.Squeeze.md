---
id: 1uayrlfqkbh57vq5t22f2wi
title: Squeeze
desc: ""
updated: 1726669378654
created: 1726669249344
---

```thinkScript
def squeeze = if TTM_Squeeze().SqueezeAlert == 0 then 1 else 0;
def sumSqueeze = Sum(squeeze, 10);
def squeezeFired = if TTM_Squeeze().SqueezeAlert[1] == 0 and TTM_Squeeze(). SqueezeAlert == 1 then 1 else 0;

AddLabel (squeezeFired, "FIRED", color.black);
AddLabel (squeeze, +sumSqueeze, color.white);
AddLabel (!squeezeFired and !squeeze, " ", color.black);

AssignBackgroundColor (if squeezeFired then color.green else if squeeze then color.red else color.black);
```
