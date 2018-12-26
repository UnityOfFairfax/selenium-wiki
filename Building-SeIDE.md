There are two different ways you can interact with the Selenium-IDE (Se-IDE) from a development perspective

# Development

Most of the time people reading this will want to use it in a 'development' mode. Working this way means you don't have to restart Firefox all the time to see changes; you just need to reload the bit of XUL that had the overlay applied to it.

In order to do this you need to...

  1. configure your Firefox profile along the lines of https://developer.mozilla.org/en/Setting_up_extension_development_environment
  1. move code around in your local copy to be 'proxy' friendly. To do this you can use the _s ide\_proxy\_setup_ task

```sh
./go ide_proxy_setup
# or 
go.bat ide_proxy_setup
```
  1. In the extensions subdirectory of your profile, create a file called {a6fd85ed-e919-4a43-a5af-8da18bda539f} and in it put the complete path to the `trunk/ide/main/src directory`
  1. Restart Firefox

**DO NOT** aggressively do an _svn add_ when running in the proxy mode and commit. It will make people cranky. A good habit is to do an _se\_ide:remove\_proxy_ and then _svn status_ and _svn add_.

# Release

When you need to ship your / the changes and need an actual XPI file, you will want to do use the _ide_ task. It will leave an XPI in `trunk/build/ide` called `selenium-ide.xpi`

```sh
go ide
```

If you are doing a proper release of Se-IDE and need it with the embedded version then the _release\_ide_ task is what you are looking for. It does _ide_ and then renames it based upon the value of ide\_version in the Rakefile.