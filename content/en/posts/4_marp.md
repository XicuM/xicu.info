---
title: How to code beautiful presentations with Marp
date: 2024-10-11T17:35:33+02:00
ShowWordCount: false
comments: true
showToc: true
draft: true
---

## What is Marp?

Marp is a tool that allows you to create beautiful presentations using Markdown. It is a great tool for developers who want to create presentations without having to worry about the design. It allows you to focus on the content and let Marp take care of the rest.

## How to install and use Marp

There are several ways to install and use Marp. The one I recommend is to use the Marp extension for Visual Studio Code. This extension allows you to create, preview and export Marp presentations directly without leaving the VS Code editor.

To install the Marp extension, follow these steps:

1. Open Visual Studio Code (if you don't have it installed, you can download it from [here](https://code.visualstudio.com/)).
2. Go to the Extensions view and earch for "Marp" in the Extensions view search box.
3. Click on the "Install" button to install the extension.

## First steps with Marp

Once the extension is installed, you can start creating Marp presentations by creating a new Markdown file and adding the following YAML front matter:

```markdown
---
marp: true
---

# Hello world 
Now you can start writing your presentation using Markdown syntax.
```

To preview the presentation, just click on the "Open Preview to the Side" button in the top right corner of the editor. 

Finally, to export the presentation, click on the "Show Quick Pick of Marp Commands" button in the top right corner of the editor and select "Export slide deck". You can choose between several formats, such as PDF, PNG, PowerPoint or HTML.

## Custom CSS themes

### My custom theme

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

<!-- Add example -->
<!-- {{< adobepdf url="Francisco_MaríPrats_CV.pdf" name="Curriculum Vitae" embedMode="FULL_WINDOW" >}} -->

If you have reached this point, you are ready to start creating beautiful presentations with Marp. Enjoy! 🚀