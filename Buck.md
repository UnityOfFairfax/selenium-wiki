#How to build with Buck - in BETA

# Building Selenium with Buck

The easiest thing to do is to just run "./go". The build process will download the right version of Buck for you so long as there's no `.nobuckcheck` file in the root of the project. The download ends up in `$HOME/.crazyfun/buck/HASH/buck.pex` where `HASH` is the value of the current buck version (given in the `.buckversion` file in the root of the project.

If you'd like to build and run our fork of Buck, then:

```
git clone https://github.com/SeleniumHQ/buck.git
cd buck && ant
export PATH=`pwd`/bin:$PATH
cd ~/src/selenium 
buck build chrome firefox htmlunit remote leg-rc
buck test --all
```


# Updating the `buck.pex`

Should you need to update the version of Buck that is downloaded:

* Checkout the source to Buck and build the PEX: `buck build --show-output buck`
* Figure out the git hash of the version you've just built. Normally that'll be the HEAD of master. Put that full hash into the `.buckversion` of the main selenium project.
* Put the md5 hash of the PEX into the `.buckhash` file in the main selenium project.
* Create a new release of SeleniumHQ's Buck fork on GitHub. The name is `buck-release-$VERSION`, where $VERSION is whatever's in `.buckversion` in the main selenium project.
* Upload the PEX to the release, and make the release public.
* Commit the changes to the main selenium project and push them.