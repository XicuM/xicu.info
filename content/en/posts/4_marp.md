---
title: How to code beautiful presentations with Marp
date: 2024-11-09T10:35:33+02:00
ShowWordCount: false
comments: true
showToc: true
cover:
   image: https://marp.app/assets/og-image.png
---

## First of all... what is Marp?

Marp is an innovative tool developed by [Yuki Hattori](https://github.com/yhatt) that simplifies creating visually appealing presentations. What sets Marp apart is its use of Markdown—a lightweight, plain text markup language known for being easy to read and write.

Markdown's straightforward syntax has made it popular among writers and developers for producing content that is both structured and readable. Marp builds on this simplicity, transforming Markdown into professional-looking slides with minimal effort.

With Marp, you can focus on your content, writing it in plain text with basic Markdown commands, without the distraction of complex design tools.

## How to install and use Marp

There are several ways to install and use Marp. The one I use is the Marp extension for Visual Studio Code. This extension allows you to create, preview and export Marp presentations directly without leaving the VS Code editor.

To install the Marp extension, follow these steps:

1. Open Visual Studio Code (if you don't have it installed, you can download it from [here](https://code.visualstudio.com/)).
2. Go to the Extensions view and earch for "Marp" in the Extensions view search box.
3. Click on the "Install" button to install the extension.

## Four simple steps to create a Marp presentation

Let's start with a simple example to show you how easy it is to create a Marp presentation, focusing for the moment on the content.

### 1. **Create the Markdown file** 
Once the extension is installed, you can jump up into creating Marp presentations by initializing a new Markdown file. You can do this by creating a new file with the `.md` extension. If it is the first time you are using Visual Studio Code, it will ask you to install the recommended extensions for Markdown highlighting and previewing, so you can easy identify titles, links and other features of the Markdown syntax.

### 2. **Enable Marp and start writing**
To enable Marp in the Markdown file, you need to add `marp: true` at the beginning of the file, wrapped in three dashes. Then, you can start writing your presentation using Markdown. [This guide](https://www.markdownguide.org/basic-syntax/) provides a detailed explanation of the basic Markdown syntax. You could start, for example, with the following code:

   ```markdown
   ---
   marp: true
   headingDivider: 1
   ---

   # Slide 1
   Now you can start writing your presentation using Markdown...

   # Slide 2
   ...and create as many slides as you need.
   ```

### 3. **Preview the content**
You can preview what you are writing at every moment. To do so, just click on the "Open Preview to the Side" button in the top right corner of the editor. 

### 4. **Export the presentation**
Finally, to export the presentation, click on the "Show Quick Pick of Marp Commands" button in the top right corner of the editor and select "Export slide deck". You can choose between several formats, such as PDF, PNG, PowerPoint or HTML.

## Advanced features

### Image embedding

## Customize your presentation with a CSS theme

### Install a theme

### Create your own theme

The following preamble is added at the beginning of the Markdown file:

```yaml
marp: true
theme: minimal
paginate: true
headingDivider: 2
style: |
   h2:before {
      /* Add the title of the presentation here */
      content: '/ Title / ';
   }
```


The complete list of Marp themes can be found [here](https://marpit.marp.app/theme-set).

some themes here: https://rnd195.github.io/marp-community-themes/


If you have reached this point, you are ready to start creating beautiful presentations with Marp. Enjoy! 🚀

https://marpit.marp.app