# Collapsing Menus in Tableau Dashboards
Template and instructions for creating a collapsible sidebar menu in Tableau dashboards.

## Introduction
In complex data visualizations, screen real estate is often at a premium. It is typically good practice to include an explanation of the dashboard's content and how it was intended to be used, but it is difficult to incorporate such an explanation without taking too much space away from the data. From a design point of view, a neat solution to this tradeoff is to place explanatory text in a sidebar that the user can expand when needed, and collapse when ready to focus on the data. However, Tableau does not provide a convenient way of implementing such functionality, so a workaround is necessary.

This repository contains a Tableau packaged workbook illustrating how to create a collapsible sidebar. It is based on the technique described in [this blog post](https://interworks.com/blog/rrouse/2016/01/04/creating-collapsing-menu-container-tableau). In addition to the workbook, which is meant to be a starting point for incorporating the sidebar into your own dashboards, the goal of this document is to provide a detailed walkthrough of the implementation step-by-step, filling in some of the gaps that the blog post skips over.

## Getting started
You will first need to create a new data source consisting of a single text file. The text file should contain one column, named "Toggle", and two rows, "show" and "hide". I used Excel to create this file and saved it as a CSV called `toggle.csv`.

Once you've created the file, connect to it in Tableau. From the **Data Source** screen, open the Data menu and choose New Data Source. Then select "Text File" and navigate to `toggle.csv`. Your **Data Source** screen should look something like this.

![Data Source for toggle.csv](img/toggle-data-source.png)

## The concept
As the blog post says, the general idea is that the dashboard will have three components laid out side-by-side. The rightmost component is the content of the dashboard itself. It can contain whatever you'd like. The center component is the sidebar. The leftmost component is a blank worksheet that is positioned off of the visible portion of the screen to the left, and can be shown or hidden when the relevant button is pressed. When it is hidden, it takes up zero horizontal space, and so the sidebar to its right becomes positioned offscreen. When it is shown, the sidebar gets pushed to the right and into the visible part of the screen, pushing the dashboard content to the right as well. This provides the "collapsible" functionality.

To get this to work, there are three components that must be set up in a very particular way. They are all worksheets, and they all connect to the `Toggle` data source described previously. The first is the blank worksheet. The other two appear to the user to be the "collapse" button and the "expand" button. These are actually worksheets, and the button-like behavior comes from a **filter action** that is created using them.

## Step 1: The show/hide sheets

1. Create a parameter named **0.0** that takes the value 0. This parameter will never be changed and is just used to correctly position the icons.
2. Drag the `Toggle` dimension into the Filters pane. Set the filter to include `show` only.
3. Drag the **0.0** parameter into the Columns pane *twice*. Then right click on the second one and select "Dual Axis".
4. In the Marks pane, expand the mark type dropdown and select "Shape". Then click Shape and choose a shape to display. This shape is what will appear as the icon the user selects to expand the sidebar. You can upload a custom image if you'd like to use the "hamburger" three-horizontal-lines icon commonly seen on mobile websites and apps. For now, just choose the `+` shape.
5. Next we need to hide everything on the sheet except for the `+` mark itself. Right click on both the top and bottom axes and deselect "Show Header". In the Marks pane under "All", click on "Tooltip" and deselect "Show tooltips". Right click on the `+` itself and choose "Format...", then go into the Format Borders tab and set everything to "None". Do the same in the Format Lines tab.
6. Adjust the size and color of the mark to your liking.
7. You may notice that hovering over the `+` causes a thick border to appear around the shape. To prevent this from happening, the trick is to set the shape for *one* of the two parameters on the sheet to a completely transparent image. There is a 100x100 transparent image included in this repository. To use it, find the folder on your machine called "My Tableau Repository" (to find its location, open the "File" menu in Tableau and select "Repository Location..."). Open it, then open the "Shapes" folder, create a subfolder named "Custom Images" or something similar, then copy the image into that new folder. From Tableau, in the Marks pane, go to "0.0 (2)" and click Shape, then "More Shapes...". You should see the name of the folder you created in the dropdown list (if not, click "Reload Shapes" or restart Tableau and check again). Your image should appear in the box. Since it's transparent, it may not look like it's there, but if you move your mouse into the box you should be able to find it. Choose the transparent image as the shape, and the `+` mark will no longer have the border when hovering over it.

![Settings for the 0.0 parameter](img/parameter-0.png)
