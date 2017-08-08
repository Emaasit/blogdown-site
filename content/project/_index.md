+++
# Projects widget.
# This widget displays all projects from `content/project/`.
title = "Projects"
subtitle = ""
widget = "projects"
date = "2017-01-01T00:00:00Z"
math = false
highlight = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = ""
caption = ""

# Order that this section will appear in.
weight = 50

# View.
# Customize how projects are displayed.
# Legend: 0 = list, 1 = cards.
view = 1

# Filter toolbar.
# Add or remove as many filters (`[[filter]]` instances) as you like.
# Use "*" tag to show all projects or an existing tag prefixed with "." to filter by specific tag.
# To remove toolbar, delete/comment all instances of `[[filter]]` below.
[[filter]]
  name = "All"
  tag = "*"
  
[[filter]]
  name = "Machine Learning"
  tag = ".machine-learning"

[[filter]]
  name = "Urban Mobility"
  tag = ".urban-mobility"

[[filter]]
  name = "Highway Safety"
  tag = ".highway-safety"
  
[[filter]]
  name = "Smart Cities"
  tag = ".smart-cities"  
  
+++