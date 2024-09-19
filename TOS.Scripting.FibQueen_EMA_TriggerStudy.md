---
id: jfz6lcuj82tnv8drhfpsizr
title: FibQueen_EMA_TriggerStudy
desc: ""
updated: 1726672798564
created: 1726672764473
---

```ts
input price = close;
input fast_length = 8;
input slow_length = 34;
input displace = 0;
def na = double.nan;

plot fastema = ExpAverage(price[-displace], fast_length);
fastema.SetDefaultColor(color.blue);
fastema.SetLineWeight(2);


plot slowema = ExpAverage(price[-displace], slow_length);
slowema.SetDefaultColor(color.dark_red);
slowema.SetLineWeight(2);


def crossover = if fastema > slowema AND fastema[1] <= slowema[1] then 1 else 0;
def crossunder = if fastema < slowema AND fastema[1] >= slowema[1] then 1 else 0;

Plot LongTrigger = if crossover then low - tickSize() else na;
Plot ShortTrigger = if crossunder then high + tickSize() else na;

LongTrigger.SetPaintingStrategy(paintingstrategy.BOOLEAN_ARROW_UP);
LongTrigger.SetLineWeight(3);
LongTrigger.SetDefaultColor(color.GREEN);
LongTrigger.HideBubble();
LongTrigger.HideTitle();
ShortTrigger.SetPaintingStrategy(paintingstrategy.BOOLEAN_ARROW_DOWN);
ShortTrigger.SetLineWeight(3);
ShortTrigger.SetDefaultColor(color.RED);
ShortTrigger.HideBubble();
ShortTrigger.HideTitle();

#Trigger alerts
alert(crossover[1], "Long Trigger", Alert.Bar, Sound.Ding);
alert(crossunder[1], "Short Trigger", Alert.Bar, Sound.Ding);
```
