# Notes on fixing [Bug 1385233](https://bugzilla.mozilla.org/show_bug.cgi?id=1385233)

1. Searched for `bootstrap.js`, found the following information sources:
    * [Bootstrapped extensions]( https://developer.mozilla.org/en-US/Add-ons/Bootstrapped_extensions)
1. If the preprocessor codes are removed from the `bootstrap.js` file, `./mach build` failed with errors about not being able to find preprocessor commands in [bootstrap.js](http://searchfox.org/mozilla-central/source/browser/tools/mozscreenshots/mozscreenshots/extension/bootstrap.js#5).

1. Somehow determined that `moz.build` was important :smiley:.
1. [Searched for "bootstrap.js" in other places on searchfox.org](http://searchfox.org/mozilla-central/search?q=bootstrap.js&path=), discovered [this](http://searchfox.org/mozilla-central/source/browser/extensions/activity-stream/bootstrap.js) which lead me to [this](http://searchfox.org/mozilla-central/source/browser/extensions/activity-stream/moz.build) from which I determined that the [moz.build](http://searchfox.org/mozilla-central/source/browser/tools/mozscreenshots/mozscreenshots/extension/moz.build) file in mozscreenshots should probably be using

    ```python
    FINAL_TARGET_FILES += [
        'bootstrap.js',
    ]

    FINAL_TARGET_PP_FILES += [
        'install.rdf',
    ]
    ```
    in stead of
    ```python
    FINAL_TARGET_PP_FILES += [
        'bootstrap.js',
        'install.rdf',
    ]
    ```
1. This was confirmed by some googling about `moz.build` files which lead to [How Mozilla's build system works](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions/How_Mozilla_s_build_system_works) which lead to [this](https://hg.mozilla.org/mozilla-central/file/default/python/mozbuild/mozbuild/frontend/context.py) which contained the information that `FINAL_TARGET_PP_FILES` is like `FINAL_TARGET_FILES` except with preprocessing. Allegedly, this info can also be found by `mach mozbuild-reference`
1. Finally, I changed the `moz.build` file and removed the dummy preprocessing from the `bootstrap.js` file, and was able to build successfully.