Watchdog
========
Python API to monitor file system events.

Example Usage
-------------

<pre>import sys
import time
from watchdog import Observer, FileSystemEventHandler
import logging

logging.basicConfig(level=logging.DEBUG)

class MyEventHandler(FileSystemEventHandler):
    def catch_all_handler(self, event):
        logging.debug(event)

    def on_moved(self, event):
        self.catch_all_handler(event)

    def on_created(self, event):
        self.catch_all_handler(event)

    def on_deleted(self, event):
        self.catch_all_handler(event)

    def on_modified(self, event):
        self.catch_all_handler(event)


event_handler = MyEventHandler()
observer = Observer()
observer.schedule('a-unique-name', event_handler, *sys.argv[1:])
observer.start()
try:
    while True:
        time.sleep(1)
except KeyboardInterrupt:
    observer.unschedule('a-unique-name')
    observer.stop()
observer.join()</pre>


Introduction
------------
Watchdog lets your Python programs monitor filesystem events as
portably as possible using:

* inotify on Linux
* FSEvents on Mac OS X
* Windows API on Windows.
* polling as a fallback mechanism

Installation Notes
------------------
1. On Windows you will need Python and pywin32 installed.

Licensing
---------
Watchdog is licensed under the terms of the
[MIT License](http://www.opensource.org/licenses/mit-license.html)

