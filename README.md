# dd-paranoia

## A paranoid wrapper for dd

It's a script that provides mechanisms for verifying what you're about to 
destroy before you destroy it:

* Shows you what you're about to do, on which source and destination
* Asks for confirmation before proceeding
* Allows you to provide an expected size and/or model name of a device so it
* Can double-check your selection and refuse if there's a mismatch
* Highlights matching device entries and points out possible duplicates
* .. and so on.

### Additional features

* Assert model and/or size of the output device matches a pattern
* Minio source support (by prefixing 'minio://' to source path)
* Decompress gzip (.gz) source on the fly whilst writing
* Use the newest file glob in a directory (-n / --newest)
* List available output devices (-l / --ls)
* Invoke sudo automatically when needed to write to output
* Auto-unmount mounts on output device using umount or devmon

You can reach me via github: [https://github.com/gammy](https://github.com/gammy)

## Requirements

 * `dd` (core-utils) and `xargs` (find-utils)
 * The usual suspects (`bash`, `awk`, `sed`, `grep`, `stat` and so on)

