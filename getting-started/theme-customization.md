# Theme Customization

## Overview

Manga+Press comes with its own child-themes based off the WordPress themes TwentyEleven through TwentyFourteen. These themes live in the`mangapress\themes`directory \(under`plugins`\). The templates that Manga+Press uses can be found under`/comics`subdirectory of each child-theme. Manga+Press can also make use of the basic WordPress templates if the Manga+Press templates aren't available in the selected theme.

By default, Manga+Press uses its own templates for the Latest Comic Page, Comic Archive Page, and Comic Post. The Manga+Press default templates can be found under`mangapress\templates`. Inside this directory is a sub-directory called`content`. This is specifically for the Latest Comic page and Comic Archive page, which works by filtering the page's content and replacing it with the generated content from these two templates.

## Tutorial: Customizing a Third-Party Theme

This example uses [Customizr](http://themesandco.com/customizr), one of the popular free themes available on WordPress.org. The example child-theme used can be downloaded \[[here](http://www.manga-press.com/uploads/2014/11/mp-customizr.tar.gz)\].

1. We start by creating a child-theme — in this case, we're using Customizr. We'll call the new theme's directory`mp-customizr`
2. Create a`style.css`file inside the`mp-customizr`directory.
3. At the top of the`style.css`file, add the following theme header:

```css
/*
Theme Name: Manga+Press-supported Child-theme for Customizr
Theme URI: http://www.manga-press.com
Description: A child-theme for Customizr that includes Manga+Press support
Version: 1.0
Author: Jess Green
Author URI: http://www.jes.gs/
Template: customizr
Tags: comics, comic theme, manga press, webcomics, online comics, customizr
*/
```

Navigate to`Appearance > Themes`in the WordPress Admin. You should see the new child-theme listed with the available themes. Go ahead and activate the theme.

1. Inside your child-theme, create a`single-comic.php`file. Open`index.php`inside the`customizr`directory, and then copy the contents of`customizr\index.php`to`single-comic.php`.
2. Add the following lines of code to`single-comic.php`below line 38 \(line 38 should be:`<?php do_action('__loop') ?>`\)

   ```php
   <?php mangapress_comic_navigation();?>
   <?php the_post_thumbnail(); ?>
   ```

Save the file, then view one of the comic pages on the frontend of your website. Your comic posts should be integrated with the Customizr theme. A complete Customizr child-theme is available for download on the Manga+Press website: \[[download](http://www.manga-press.com/uploads/2014/11/mp-customizr.tar.gz)\].

### Some Common Pitfalls

#### Broken Theme Layout

If you're experiencing unexpected output or skewed layouts \(Manga+Press-related content output doesn't fit the theme\), extending your chosen theme with a child-theme using Manga+Press' templates is recommended.

For the Comic Post view, try copying the`single.php`template from the your child-theme's parent and renaming it`single-comic.php`, then adding`mangapress_comic_navigation()`inside the main loop of the template, ideally below`the_title()`call.

#### Navigation doesn't appear correctly or at all

Confirm that the navigation element is being generated by viewing the page's source-code in the browser \(usually right-click and select "View Source"\). If the navigation element is present in the source \(look for something like`<nav class="comic-navigation"></nav>`\), check and make sure that there are no rogue styles in the parent theme that is hiding the nav element.

Check and make sure that the`mangapress_comic_navigation()`call is inside the template's main loop.

Finally, if the navigation is showing up but is displaying incorrectly, then you may need to add the navigation styles to your theme:

```css
/* comic navigation */
.comic-nav-hlist-wrapper {
    text-align: left;
    margin: 5px 0 10px 0;
    padding: 0;
    clear: both;
    float: none;
}

.comic-nav-hlist {
    list-style: none;
}

.comic-nav-hlist > li {
    float: left;
    margin-right: 10px;
}
```

