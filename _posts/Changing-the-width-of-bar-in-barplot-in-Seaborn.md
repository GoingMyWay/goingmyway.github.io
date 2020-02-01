---
title: Changing the width of bar in barplot in Seaborn
date: 2018-11-12 18:40:39
tags: Python
categories: Python
---

By getting the patch attribute of `ax` and modify the width of each patch you can change the width of barplot, remmember to reset coordinates of re-shaped bars.

```Python
import matplotlib.pyplot as plt
import seaborn as sns


def change_width(ax, new_value) :
    for patch in ax.patches :
        current_width = patch.get_width()
        diff = current_width - new_value

        # we change the bar width
        patch.set_width(new_value)

        # we recenter the bar
        patch.set_x(patch.get_x() + diff * .5)

tips = sns.load_dataset("tips")
fig, ax = plt.subplots()

sns.barplot(data=tips, ax=ax, x="time", y="tip", hue="sex")
change_width(ax, .35)
plt.show()
```

Reference: https://stackoverflow.com/a/44542112/5046896
