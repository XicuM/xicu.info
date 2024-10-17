# My personal website

This is the source code of my personal website. It is built with [Hugo](https://gohugo.io/) and the [Hugo Papermod theme](https://github.com/adityatelange/hugo-PaperMod?tab=readme-ov-file).

## Developer notes

### Server

To run the server with drafts and future posts, use the following command:

```bash
hugo server --ignoreCache -D
```

### Add themes

To add a theme as a submodule, use the following command:

```bash
git submodule add --depth=1 url_to_theme themes/theme_name
```

The features of this theme are described in [PaperMod's Wiki](https://github.com/adityatelange/hugo-PaperMod/wiki).

### Deploy the website in GitHub Pages

Create the `.github/workflows` folder and add the `hugo.yml` file with the content of this [link](https://gist.githubusercontent.com/thisismikekelly/1a24ad2c8c923127dc3cb29edca13746/raw/f5d449a0aca3d33b88825e563734e6d782752e4a/hugo.yaml).

### To Dos

- [x] Add gallery shortcode
- [ ] Finish projects section
- [ ] Include images in About me section
- [ ] Finish contact form: https://www.formbackend.com/hugo-contact-form
- [ ] Improve footer
- [ ] Hamburguer menu: https://www.youtube.com/watch?v=U8smiWQ8Seg
- [ ] Subscribe button
- [ ] Consider migrating to Astro