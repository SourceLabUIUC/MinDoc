# MinDoc: Create Your Own Digital Documentary Edition

## What is MinDoc?
MinDoc is a simple publishing template that can be used to create electronic editions of historical sources (texts, images, film). Inspired by the 'minimal computing' movement, it is aimed at anyone who is looking for a basic, open platform for sharing documents they have digitized. MinDoc makes it easy to develop a simple static web page where you can display and describe your materials, in a form that can be used by researchers, teachers, and the public at large. No coding experience is required (though you'll learn a few basic skills along the way). MinDoc is also designed to help you meet the Minimum Standards for Electronic Editions developed by the Association for Documentary Editing, so you'll know your readers have what they need to work with the material you're presenting. 

---

## Key Concepts (Start Here if You're New)

Before you begin, here are a few terms you'll see throughout this guide. You don't need any technical background, just a general sense of what these mean.

**GitHub** is a free website where people store and share project files. Think of it as a combination of cloud storage and a publishing platform. You'll use it to hold your edition's files and to put your finished site online, all for free.

**Repository (or "repo")** is the name for a single project on GitHub. It's essentially a folder that holds all the files for your edition, your text, images, and settings, in one place. When you make your own copy of MinDoc, you're creating your own repository.

**Static web page** is the kind of website MinDoc creates. "Static" means the pages are built ahead of time and simply displayed to visitors, rather than changing on the fly. This is exactly what a digital edition needs, and it's why the site can be hosted for free and load quickly.

**GitHub Pages** is the GitHub feature that turns your repository into a live website on the internet. Once you turn it on, GitHub takes the files in your repo and publishes them at a web address you can share. This is the step that makes your edition public.

---

## Getting Started with MinDoc on GitHub

This guide assumes you have **no prior GitHub experience**. If you're already familiar with GitHub, feel free to skip ahead. Typical technical information will be found below.

### Step 1: Create a GitHub Account
Sign up for a free GitHub account at [github.com](https://github.com) by selecting the **Sign Up** button at the top of the page.

### Step 2: Create Your Own Copy of MinDoc

A **template** is a ready-made starting point. MinDoc is set up as a template repository, which means you can create your own complete copy of it with a single click, then change it however you like without affecting the original.

1. Scroll to the top of the MinDoc template repository
2. Find the **"Use this template"** button (it looks like this):

<img width="209" height="59" alt="Use this template button" src="https://github.com/user-attachments/assets/5b3fd054-33c7-421f-899f-1083ce44a9e6" />

3. Click it and select **"Create a new repository"**

### Step 3: Name Your Repository
Choose a simple, descriptive name for your repository. The name you choose will become part of your website's URL so you might want to use a version of your publication's title. (e.g., `the-correspondance-of-george-washington-yyyy-yyyy`, `The-Epistolary-Presidency`, `scenes-from-mount-vernon`). A clear name helps others understand what your project contains. Repository names have some restrictions that might prevent you from using your publication's full title or using the exact title. It is possible to change the repository name later. 

MinDoc also uses this repository name automatically to build your site's web address, so you won't need to configure the address yourself later.

### Step 4: Click "Create Repository"
You should now have your own copy of MinDoc attached to your GitHub account. You'll see a screen like this:

<img width="356" height="336" alt="Newly created repository" src="https://github.com/user-attachments/assets/d8e095ca-4534-4730-82e2-0e467fc3ec93" />

### Step 5: Enable GitHub Pages

A **branch** is a version of your repository's files. Every repository starts with one main branch (called "Main"), which holds the official, current version of your project. For MinDoc, you'll simply publish your site from this Main branch.

1. Go to your new repository's **Settings** tab
2. Select **"Pages"** from the left menu
3. Under "Build and deployment," select **"Deploy from a branch"**
4. Choose **"Main"** as your branch

**Your site is now live!** GitHub will provide you with a URL (usually `yourname.github.io/repository-name`) where your digital edition will appear.

---

## How to Use MinDocMini

### Edit Your Site Title and Description
**File:** `_config.yml`

Open this file and update:
```yaml
title: Your Document Title
description: by Your Name
```
These yaml fields will modify the title and description fields on your web page.

**Note:** You do **not** need to edit the `baseurl` setting in this file. MinDoc automatically uses your repository's name to build your site's web address, so leaving `baseurl` empty is correct for almost everyone. (Advanced users who need a custom address can set it manually, but this is rarely necessary.)

### Add Your Main Content
**File:** `index.markdown`

This file contains all the text for your website. Use standard Markdown formatting:
- `# Heading` = Main section title
- `## Subheading` = Subsection
- `**Bold text**` for emphasis
- Write paragraphs normally

Example:
```markdown
# My Digital Edition

## Edition Overview
This edition includes photographs and documents from...

## First Section
Information about the first theme or time period...
```

### Add Images to Your Edition

#### 1. Upload Image Files
Place your image files in the `assets/img/` folder. Use clear filenames (e.g., `letter-1850.jpg`, `photograph-main.png`).

#### 2. Create an Image Description File
For each image, create a new file in the `_mindoc_media/` folder with the same name but ending in `.md`

**Example:** `_mindoc_media/letter-1850.md`

```yaml
---
page: source  ## DO NOT CHANGE THIS FIELD
title: Penny Magazine Rooks 
media_type: image

_title: Penny Magazine Rooks
description: A full magazine page image featuring the title "Monthly Supplement of the Penny Magazine of the Society for the Diffusion of Useful Knowledge," and the dates, December 31, 1839, to January 31, 1839. Below this information is an engraving print image of trees with nesting rooks labeled "a rookery," followed by two columns of magazine text.
creator: Society for the Diffusion of Useful Knowledge
_date: January 31, 1839
rights: Public Domain
type: StillImage
source: University of Iowa
identifier: https://babel.hathitrust.org/cgi/pt?id=iau.31858046224600&seq=553 Volume p. 33, Digitization #41
contributor: Society for the Diffusion of Useful Knowledge
format: v ill 29 cm, jpg
credit_(IPTC): Digitization courtesy Google, HathiTrust Digital Library
date_created_(IPTC):

_path: /assets/img/main_page.jpg ##This field should point to the IMAGE you want to bring into your web page.
order: '03' ##This field determines the order that the image will appear on the page. Start at 01, 02, 03... etc.
layout: image_description ##DO NOT CHANGE THIS FIELD
---

---
```

**What each field means:**
- `page:` - The section where this image appears (must match a section in your content)
- `media_type:` - Type of content (usually "image")
- `order:` - Display order (1 = first, 2 = second, etc.)

#### 3. Display Images in Your Content
In your `index.markdown` file, add this code where you want images to appear:

```liquid
{% assign media = site.mindoc_media | where: "page", "source" %}
{% include media_next.html pages=media %}
```
The first line sets up the ability to call images into the page. It can go anywhere, as long as it is before you use the second line and you only need to use it once. The second line can be repeated everywhere you want an image. It will add images based on the value in the 'order' field.
---

## Troubleshooting (FAQ & Common Issues)

**Q: My site isn't showing up**
- Check the Actions tab to see how your deployment is going when you make a change.
- Wait 2-3 minutes after enabling GitHub Pages for the site to deploy
- Check that you selected "Main" branch in Settings > Pages

**Q: Images aren't displaying**
- Make sure that your images are no larger than 1200px by 1920px
- Check that image filenames match exactly in your `.md` files
- Verify images are in the `assets/img/` folder
- Check your liquid code. The second line brings in the actual using the order value in the file metadata. The first line sets this process up. The first line can go anywhere as long as it is before you try calling in an image.
- You should **not** need to change the `baseurl` setting in `_config.yml`. MinDoc sets your site's web address automatically, so an empty `baseurl` is correct. Only change it if you intentionally need a custom address.

**Q: How do I make edits after publishing?**
- Edit files directly in GitHub by clicking the pencil icon
- Changes deploy automatically within a few minutes

---

## Technical Information

### Tech Stack
- **HTML**: 61.5% - Markup structure
- **SCSS**: 25.3% - Styling and theming
- **Ruby**: 13.2% - Jekyll-based site generation

### Requirements
- [Git](https://git-scm.com/) for version control
- [Jekyll](https://jekyllrb.com/) - A static site generator built with Ruby
- [Ruby](https://www.ruby-lang.org/) 2.7 or higher

### Installation (for developers)

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/your-repository-name.git
   cd your-repository-name
   ```

2. Install dependencies:
   ```bash
   bundle install
   ```

3. Run locally:
   ```bash
   bundle exec jekyll serve
   ```

4. Visit `http://localhost:4000` in your browser

### Project Structure
```
├── _config.yml          # Site configuration
├── _mindoc_media/       # Image metadata files
├── assets/
│   └── img/            # Image files
├── _includes/          # HTML template components
├── _layouts/           # Page layout templates
├── index.markdown      # Main content file
└── README.md          # This file
```

## Credits

MinDoc is built on [Jekyll](https://jekyllrb.com/), a static site generator.

MinDoc was developed for classroom use by members of SourceLab at the University of Illinois Urbana-Champaign. The original project team included Liza Senatrova, John Randolph, Caroline Kness, and Richard Young.

For more help with Markdown, visit [Markdown Guide](https://www.markdownguide.org/).
