## Installing Zbar (for Python only, no Qt or GTK) - OS X 10.6.8
================================================================
1. Download and uncompress the latest [zbar](http://zbar.sourceforge.net/download.html) source.
2. Don't try to install it in a directory with spaces in the name...
3. `$cd zbar-0.10`
4. Configure zbar:
	- *If you've never upgraded Python* (default Apple python 2.6.1 build):
```bash
./configure --disable-video --without-jpeg --without-imagemagick --without-gtk --without-qt --without-java CFLAGS='-arch x86_64 -Os -pipe' PYTHON_CFLAGS='-I/System/Library/Frameworks/Python.framework/Versions/2.6/include/python2.6 -I/System/Library/Frameworks/Python.framework/Versions/2.6/include/python2.6 -fno-strict-aliasing -fno-common -dynamic -DNDEBUG -g -fwrapv -Os -Wall -Wstrict-prototypes -DENABLE_DTRACE -arch x86_64'
```
	- If you've upgraded to Python 2.7 via brew (see <https://github.com/gjoseph92/installing/blob/master/OpenCV-Python-Homebrew.md>):
```bash
./configure --disable-video --without-jpeg --without-imagemagick --without-gtk --without-qt --without-java CFLAGS='-arch x86_64 -Os -pipe' PYTHON_CFLAGS='-I/usr/local/Cellar/python/2.7.4/Frameworks/Python.framework/Versions/2.7/include/python2.7 -I/usr/local/Cellar/python/2.7.4/Frameworks/Python.framework/Versions/2.7/include/python2.7 -fno-strict-aliasing -fno-common -dynamic -DNDEBUG -g -fwrapv -Os -Wall -Wstrict-prototypes -DENABLE_DTRACE -arch x86_64'
```
	(I haven't actually tested this...)
5. `make`
6. `sudo make install`

----------
If you get errors about the architecture (x86_64), try replacing `x86_64` in the `configure` command with `i386` (note it occurs twice!). The [original instructions](http://sourceforge.net/p/zbar/discussion/664595/thread/875f2242) use `i386`, which gave me an error.