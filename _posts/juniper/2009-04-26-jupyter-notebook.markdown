---
layout: post
title:  "jupyter-notebook"
date:   2009-04-26 20:49:38 +0400
categories: juniper
tags: juniper
---

# jupyter-notebook
mkdir envcour
  910  virtualenv -p python3 envcour
  911  source envcour/bin/activate
  913  pip install --upgrade pip
  914  pip3 install pandas
  915  pip3 install notebook
  918  pip3 install widgetsnbextension
jupyter notebook --ip='127.0.0.1' --port=49151
