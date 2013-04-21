## OpenCV Installation via Homebrew (Python 2.7.4, OS X 10.6.8)

What seems to go wrong in OpenCV installations from `brew` involves the different instances/version of Python you often have on your machine: OpenCV binds to one in installation, but not the one `which python` references. Then `import cv` causes a segfault. Great. One way to avoid this is to _never update python_ (keep the default OS X version), but that makes installing any python libraries (which no longer offer 2.6 binaries) much harder. So here's how to upgrade to Python 2.7.4 and install OpenCV via `brew`.
---------------------------
1. Clean out everything. Any Python libraries will have to be reinstalled for the new version. This means removing `/usr/local/lib/python2.7`, `/usr/local/opt/python`, `/usr/local/bin/python*`, if they exist, `brew rm python` if you brewed it already, etc. `python` should open Apple python 2.6, `which python` should give you `/usr/bin/python`. Also delete everything OpenCV-related in `/usr/local`. We want a clean slate.

2. Make `/usr/local/bin` the *first* thing in your `PATH`. It definitely has to precede `/usr/bin` (otherwise you'll still get default python over the brewed one), but putting it first seems most reliable. So (`sudo`) edit `/etc/paths` (which specifies the default `$PATH` before anything in your `.bash_profile' gets to) and move `/usr/local/bin` from the bottom to the top. Then modify any path additions in `.bash_profile` to post-pend the new path (`export PATH="/new/path:$PATH"` --> `export PATH="$PATH:/new/path"`) so `/usr/local/bin` stays first. You could _probably_ just add `export PATH="/usr/local/bin:$PATH"` to the very end of `.bash_profile`, but this definitely works and avoids the double-including.

3. `brew install python`. Once it's done, try `python` in a _new_ Terminal window and make sure it's 2.7 (the current one will still be 2.6 unless you `source ~/.bash_profile`). Also make sure that `otool -L Cellar/python/2.7.3/Frameworks/Python.framework/Python` gives you
	/homebrew/Cellar/python/2.7.3/Frameworks/Python.framework/Versions/2.7/Python (compatibility version 2.7.0, current version 2.7.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 169.3.0)

4. To avoid future weirdness, update basic Python libraries before OpenCV installs with them. Brew installs pip, so `pip install numpy`, `pip install matplotlib`, etc. Or just download the binaries and install them.

5. `brew install opencv`. Note: you have to `brew tap homebrew/science` first.

6. Open python, `import cv`, and marvel at the lack of segfaulting!

If that doesn't work, it's probably because your `PATH` didn't have `/usr/local/bin` as the first thing since before you brewed python up through installing OpenCV. Uninstall everything and start over. `brew rm $(brew deps opencv)`, `brew rm opencv`, `brew rm $(brew deps python)`, `brew rm python`, delete any stray files, make sure `brew doctor` has no (relevant) warnings, then follow step 2. `echo $PATH` and make sure that `/usr/local/lib` is the very first thing before proceeding.
------------------------------
Gabe Joseph, April 2013.
Based on <https://github.com/mxcl/homebrew/issues/16016#issuecomment-10361450>, <https://github.com/mxcl/homebrew/pull/12758>, and <https://github.com/mxcl/homebrew/wiki/Common-Issues>.