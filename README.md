Using Ports
-----------

In FreeBSD 10, there's currently no official pkgng repo setup to
distribute binary packages. The following tips should make it
easier to compile from source.

* If building for a single system, go ahead and set your
  processor type in `/etc/make.conf` using the _CPUTYPE_
  variable. For a full list of processors, see 
  `/usr/share/examples/etc/make.conf`. As an example,
  here's the line I use.

        CPUTYPE=k8

* Put your working directory into RAM by creating `/ram` as
  root and adding an entry to fstab.

        tmpfs 	/ram	tmpfs	rw	0	0

  You'll also need to explicity set your working directory
  in `/etc/make.conf` with the following line.

        TMPWRKPREFIX=/ram

* To aid compile time, one of the first packages I install is 
  `/usr/ports/devel/ccache`. After the build is complete, just
   add the following line to your `/etc/make.conf` to enable 
   ccache.

        WITH_CCACHE_BUILD=yes

* Instead of selecting your config options at compile time,
  use `make config-recursive` to configure the current port
  and all of its dependencies.

* Always `make install clean` when building packages, especially 
  if using a working directory located in tmpfs.

