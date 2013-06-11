Installing PyOpenNI on OS X, based on OpenNI 1.5.4 and Homebrew Python and Boost
================================================================================
[PyOpenNI](https://github.com/jmendeth/PyOpenNI) is a Python wrapper for the [OpenNI](http://www.openni.org) middleware, which exposes a (not-so-pleasant) interface for getting depth, skeleton, and rudimentary gesure data. As a prerequisite, you need to install OpenNI. However, the new and cleaner version of OpenNI has no Kinect support, making it vaguely useless, therefore you'll want to download the [previous versions](http://www.openni.org/openni-sdk/openni-sdk-history-2/) of OpenNI and NITE for Mac. Installing the Python bindings also requires Boost, and for clenliness, use a clean, brewed install of both.
Steps
-----
1. If you don't have Boost already, the best approach is to brew to a updated version of Python, and install Boost via brew. If you haven't installed Python via Homebrew (i.e. you have Apple Python 2.6), follow steps 1-4 of the [OpenCV installation guide](https://github.com/gjoseph92/installing/blob/master/OpenCV-Python-Homebrew.md). Everyone likes a clean, well-lighted brew.

2. Now that everything is nicely configured, `brew install boost` should work slowly, but without errors.

3. Once you have Boost linked against Python, install [OpenNI and NITE](http://www.openni.org/openni-sdk/openni-sdk-history-2). Unpackage the tarballs you downloaded (you did download them, right?). First, in the OpenNI directory, just `sudo ./install`, then do the same in the NITE folder. (It should seem that fast and painless, it just copied a few files.)

4. If you don't have cmake (you probably do), you'll need it. Just `brew install cmake`.

5. Download PyOpenNI via `git clone https://github.com/jmendeth/PyOpenNI.git`. Don't go into the PyOpenNI directory yet! Instead, `mkdir PyOpenNI-build` next to the PyOpenNI folder, and `cd PyOpenNI-build`.

6. In there, `cmake ../PyOpenNI -DPYTHON_LIBRARY="`brew --cellar python`/2.7.4/Frameworks/Python.framework/Versions/2.7/Python" -DPYTHON_INCLUDE_DIR="`brew --cellar python`/2.7.4/Frameworks/Python.framework/Versions/2.7/Headers"`. Replace both `2.7.4`s with whichever version of Python you're using (what's listed when you run `python`).

 7. cmake will prepare the makefiles for you. If something goes wrong here, it's likely because you didn't brew Python correctly, or didn't link Boost against the right (brewed) Python. The best option is probably to uninstall everything (`brew rm python`, `brew rm boost`, etc.) and follow steps 1 and 2 carefully.

8. Run `make` to compile everything. When it finishes, you'll find the finished module at `lib/openni.so`.

9. Install it globally by moving the module into the appropriate `site-packages` directory. For me: `mv lib/openni.so /usr/local/lib/python2.7/site-packages`.

------------------------------
Gabe Joseph, June 2013.