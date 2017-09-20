# How to submit patches to mozilla

## [READ ME](https://mozilla-version-control-tools.readthedocs.io/en/latest/mozreview/commits.html#submitting-commits-for-review) THIS IS THE AUTHORITY. IF IT CONFLICTS WITH THIS DOCUMENT IN ANY WAY, IT WINS

## My steps
1. **Before you start to work**, run `hg pull central; hg update` to get the latest changes
1. FIX YER BUG
1. Make sure that everything still works locally.
1. _Pull updates again._ You must do this before you commit your bug. Not doing so will result in conflicts / having to do merges which will likely go wrong / be bad some other way.
1. commit your bug. You should use the following format for your commit message
    ```
    Bug <Bug Number> - <WHAT YOU DID>. r?<reviewer>
    ```
    replacing `<...>` with the appropriate values
1. Push to the try servers
1. If it works, then follow the instructions in the above document.
