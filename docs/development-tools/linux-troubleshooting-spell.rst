=============================
Linux troubleshooting spells
=============================

I sincerely wish the reader not to use these spells ever. They are only used when you are lost in a unknown server
where you need to troubleshoot it to find out what is wrong.

Space disk checking
********************

.. code-block:: console

    $ df -kh /opt/java11/

    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/Volgroup01-lx_root
                           19G   15G  2.9G  84% /

.. code-block:: console

    $ du -hx --max-depth=1n /opt/java11/ | sort -hr

    297M	/opt/java11/
    220M	/opt/java11/lib
    77M	/opt/java11/jmods
    544K	/opt/java11/legal
    512K	/opt/java11/bin
    228K	/opt/java11/include
    140K	/opt/java11/conf

.. code-block:: console

    ls -lrth /opt/java11/
    total 28K
    -rw-r--r--.  1  668  668 1.2K Aug 23  2018 release
    drwxr-xr-x.  2 root root 4.0K Apr 22  2021 bin
    drwxr-xr-x.  4 root root 4.0K Apr 22  2021 conf
    drwxr-xr-x.  3 root root 4.0K Apr 22  2021 include
    drwxr-xr-x.  2 root root 4.0K Apr 22  2021 jmods
    drwxr-xr-x. 72 root root 4.0K Apr 22  2021 legal
    drwxr-xr-x.  6 root root 4.0K Apr 22  2021 lib

