# dockcheck
Identifies docker containers that were built from outdated images.

For each container:
* Identify the container's ancestor images.
* Collect the names/tags of those images that have them.
* Pull the current version of each named image.
* Compare each image's build timestamp with that of the container.
* If any such image was built more recently than the container, report
  that the container needs rebuilding.

By default, this script prints output only if a container needs rebuilding or
an error occurs. This makes it work well with the cron daemon, which will run
the script regularly and email an administrator if something needs attention.

Example crontab:

    MAILTO=root
    0 2 * * * /path/to/bin/dockcheck

Caveat: I have only tested this on a small rootless docker instance with a
handful of simple containers. I might have missed something, and you might
need to tweak the script to make it work in a different environment.
