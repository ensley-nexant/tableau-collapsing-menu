# Collapsing Menus in Tableau Dashboards
Template and instructions for creating a collapsible sidebar menu in Tableau dashboards.

## Introduction
In complex data visualizations, screen real estate is often at a premium. It is typically good practice to include an explanation of the dashboard's content and how it was intended to be used, but it is difficult to incorporate such an explanation without taking too much space away from the data. From a design point of view, a neat solution to this tradeoff is to place explanatory text in a sidebar that the user can expand when needed, and collapse when ready to focus on the data. However, Tableau does not provide a convenient way of implementing such functionality, so a workaround is necessary.

This repository contains a Tableau packaged workbook illustrating how to create a collapsible sidebar. It is based on the technique described in [this blog post](https://interworks.com/blog/rrouse/2016/01/04/creating-collapsing-menu-container-tableau). In addition to the workbook, which is meant to be a starting point for incorporating the sidebar into your own dashboards, the goal of this document is to provide a detailed walkthrough of the implementation step-by-step, filling in some of the gaps that the blog post skips over.

## Getting started
You will first need to create a new data source consisting of a single text file. The text file should contain one column, named "Toggle", and two rows, "show" and "hide". I used Excel to create this file and saved it as a CSV called `toggle.csv`.

Once you've created the file, connect to it in Tableau. From the **Data Source** screen, open the Data menu and choose New Data Source. Then select "Text File" and navigate to `toggle.csv`. Your **Data Source** screen should look something like this.

[screenshot here]
