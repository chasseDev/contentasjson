# contentasjson

1. [Description](#1-description)
2. [Screenshots](#2-screenshots)
3. [Installation](#3-installation)
	3. [Manually](#manually)
5. [Credits](#5-credits)
6. [License](#6-license)

## 1. Description

This is an extension of the [Drupal Content As JSON module](https://www.drupal.org/project/contentasjson). It adds a new function that automatically builds navigation menus.

* Works on Drupal 7.

## 2. Screenshots

You can build a top navigation

![ScreenShot](https://raw.githubusercontent.com/EddyVerbruggen/SocialSharing-PhoneGap-Plugin/master/screenshots/screenshot-ios7-share.png)

And / or you can build a side navigation

![ScreenShot](https://raw.githubusercontent.com/EddyVerbruggen/SocialSharing-PhoneGap-Plugin/master/screenshots/screenshot-wp8-share.jpg)

## 3. Installation

### Manually

1\. Grab the code from this repo and add it into your Drupal 7 site
```xml
../sites/all/modules/[add-code-here]
```

2\. Find the module on your Drupal site: /admin/modules


3\. Add some custom javascript functions in your theme's main page
```xml
../sites/all/themes/[your-theme]/theme/system/page.tpl.php
```

```html
<script type="text/javascript">
    (function ($) {
      $(window).load(function () {

        var site_name = "[whatever-your-site-dir-is]/";

        function displayMenu(data) {
          $("#top-menu").children().remove();
          $("#menuContainer").children().remove();
          $("#sideNavCMS").children().remove();

          $.each(data, function(key, value) {
            var link = "content/"+value.nid;

            $('#top-menu').append('<li><a href="'+site_name+link+'" >&nbsp;'+value.title+'<\/a><\/li><li class="pipe-line">|<\/li>');
            $('#sideNavCMS').append('<li class="nav-header panel">'+
              '<a href="'+site_name+link+'" class="all-caps">'+value.title+'<\/a>'+
              '<\/li>'+
              '<li class="nav-divider"><\/li>');

            $('#menuContainer').append('<div class=" main-menu-link">'+
              '<a href="'+site_name+link+'">'+
              '<div class="home-menu-item"><span class="home-link">'+value.title+'<\/span><\/div>'+
              '<\/a><\/div><div class="separate-border"><\/div>');

          });
        }

        $(function() {
          $.getJSON(site_name+"contentasjson/menu/[whatever-content-type-you-want]", function(data) {
            displayMenu(data);
          });
        });

     });
   })(jQuery);
  </script>

```

## 5. Credits ##

This plugin was enhanced for Drupal 7 by the Chasse Development Team.


## 6. License

[The MIT License (MIT)](http://www.opensource.org/licenses/mit-license.html)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
