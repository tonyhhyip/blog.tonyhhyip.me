---
layout: post
title:  "Using Jupyter notebook for internal operator"
date:   2020-04-16
---

![Jupyter Logo](/assets/2020/04/16/Jupyter-1.webp)

Since I am going to leave the company and I would like to provide the UI for internal operator who have no idea in coding, making it available on the Angular console would take up long time, so Jupyter came into my mind.

Using Jupyter, I could directly write script for operator. The operator could just click the “run” button the selected section of the script to perform what they would like to perform and modify the parameter easily thanks to the great easy-to-read syntax of Python.

In order to prevent caseless remove of detail operation script, I put those script into a Python module and import it in the notebook, so that the script display on the notebook for the operator is just a call of function.

Jupyter could be a kind of tool to provide a simple interface for those internal operator who don’t know coding, but though a well-designed web console would be great.
