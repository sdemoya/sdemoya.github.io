---
title: "Matplotlib"
date: 2020-09-27
tags: []
header:
  image: "/images/perceptron/percept.jpg"
excerpt: "Coming soon..."
mathjax: "true"
---

# Data Visualization with Matplotlib

Allow me to demonstrate a few simple visualizations created with Matplotlib,
a mathmatical plotting library. 

### Plotting a Simple Line Graph

Python Code Block:
```python
import matplotlib.pyplot as plt

x_values = range(1, 5)
y_values = [x**3 for x in x_values]


plt.style.use('seaborn')

# fig represents the entire figure
# ax represents a single plot within the figure
fig, ax = plt.subplots()
ax.scatter(x_values, y_values, s=15)


# Set titles
ax.set_title('Cubed Numbers', fontsize=24)
ax.set_xlabel('Value', fontsize=15)
ax.set_ylabel('Cube of Value', fontsize=15)


# Define range of axes
ax.axis([0,5, 0, 125])


# Open figure in Matplotlib's viewer
plt.show()
```

Output from Matplotlib's Viewer:
<img src="{{ site.url }}{{ site.baseurl }}/images/2020-09-27-matplotlib/cubes.png" alt="simple line graph">

