About
=====
This module is the default "glue" module (D7) that Real Tidings uses to create [custom drupal websites](http://realtidings.com). We install a modified version of this module on our client websites, and then have an easy and convenient place to drop any custom code or hooks.

Installation
============
Just upload to sites/all/modules, then enable! This module provides a few features out of the box:
* Creates a custom function called **mydpm()**. This acts as a wrapper for the Devel module's *dpm()* function. The difference is that it checks to see if *dpm()* exists (ie. if Devel is turned on). If so, it uses it... if not, it simply uses a *print_r* funtion. This is to keep us from accidentally killing the site if an errant *dpm()* is turned on. See http://realtidings.com/blog/12/Apr/23/drupal-devel-dpm-bork-and-no-devel-module for details.
* Page alter to add our little (very little - 8pt) signature to the bottom of the site's pages. We also have a cool switch that adds a custom message to the bottom of admin pages (in this case, links to get support). **Be sure to at least change these if you use this module!** Otherwise, you will be adding *our signature* and links to your site.

Customize this each time you use it
==============================
First - you need to customize this to brand it for your site or your business. Thats just a no brainer:
* Rename all the files/folders and replace the "rt" with whatever you want the module to be called. (ex. mymodule)
* Then do a find and replace in the files to replace "rt_" for whatever you want your module to be. Keep the underscore! (ex. mymodule_)
* Edit the .info file description
* Edit the .module file comments
* Edit the hook_page_alter() for your links and messages.

Second - you should customize this for EACH site you use it on. This will help you keep it clear about what changes may be in one site versus another. So, when we use this for client XYZ, I will rename the module to **rt_xyz** and then change things accordingly. This may seem like its unneccessary, but trust me... it will make your life much easier.

Thirdly - the module comes with its own included CSS file (applied to a site) and optional JS file (uncomment the line in the .info). These are empty for now, but again, can be a really easy way to override or add to the site without touching a contrib theme or module.

Fourthly (?) - If you plan to add alot of code, it may be easier to create include files for each item, especially if they are long:
* hook_form_alter (if you have lots of changes)
* hook_menu
* custom forms
* 3rd party APIs or code
You should really evaluate if these need to be in their own modules... but keep in mind that keeping things clean and easy to read (good comments FTW) will make it easier for you to maintain this code in the future. If you do create include files for additional code, just use the ** module_load_include()** function like this:
```  
// this includes the file rt.form_alter.inc file
module_load_include('inc', 'rt', 'rt.form_alter');
```

Feedback
===========
If you think there is some additional code that EVERY site should have and needs to be included - let me know. 