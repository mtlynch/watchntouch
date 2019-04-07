# watchntouch

This is essentially a horrible hacky solution to the fact that CIFS mounts cannot forward file-system event to inotify on linux. This in turn makes it so any number of "on-demand" compilers (e.g. compass, coffee-script) stop working when applied to mounted shares (among other things).

The idea is to use the watchdog library to monitor a given directory using shitty-old polling, and then poke at the local filesystem so that inotify (and hopefully your apps/tools) pick up the changes. It is almost certainly a very bad idea to run this on a large file structure and/or over a slow network.

Also note that only modification events can sanely be simulated this way. If you absolutely need some form of rm or mv event simlation, you may enable a less-then-sane behavior for such things using `--simulate-rm` and `--simulate-mv` respectively.

## To run

```bash
pip install --requirement requirements.txt
./watchntouch.py
```
