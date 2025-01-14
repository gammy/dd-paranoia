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

## Additional features

* Assert model and/or size of the output device matches a pattern
* Minio source support (by prefixing 'minio://' to source path)
* Decompress gzip (.gz) source on the fly whilst writing
* Use the newest file glob in a directory (-n / --newest)
* List available output devices (-l / --ls)
* Invoke sudo automatically when needed to write to output
* Auto-unmount mounts on output device using umount or devmon

## Help

(This README document may be out of date - best check the script itself)

```
Usage: dd-paranoia -i <input file> [-o <output device>] [...]

Examples:
  Use 'foo' as input, '/dev/mmc0' as output:
   $ dd-paranoia -i foo -o /dev/mmc0
  Use 'foo' from minio alias store as input, '/dev/mmc0' as output:
   $ dd-paranoia -i "minio://store/foo" -o /dev/mmc0
  Use 'foo' as input, select output interactively:
   $ dd-paranoia -i foo
  Assert that the output device model begins with "Samsung" followed by "SSD":
   $ dd-paranoia -m "^Samsung.*SSD" -i foo -o /dev/mmc0
  Assert output device size:
   $ dd-paranoia -s "250G" -i foo -o /dev/mmc0
  Use the latest file matching a pattern in a directory (which is scanned recursively) on MinIO and prompt for output selection:
   $ dd-paranoia -i "minio://store/foo/" -n "*daily*.raw.gz"
  List available output devices and highlight Samsung models:
   $ dd-paranoia --ls -m Samsung

If no output device is specified, you will be asked interactively.

Options:
  -i <s>, --input <file>         Use <file> as the source to write. Files with a '.gz' suffix get decompressed. To access a Minio service, prefix <file> "minio://". Default: (none)
  -n <p>, --newest <pattern>     Treat -i as an input directory and pick the newest file matching <pattern>, as expressed in a glob. Default: no
  -o <d>, --output <device>      Write the source to <device>. Default: ask
  -B <p>, --mc-bin <path>        Override MinIO CLI binary with <path>. Can also be set by MINIO_CLI_BIN. Default: mccli
  -s <s>, --device-size <size>   Verify that <device> size is <size>. The format of <size> is the same as 'lsblk' or dd-paranoia's output. Default: (any)
  -m <m>, --device-model <model> Verify that the model name of <device> matches regular expression <model>, as expresssed with 'grep -P', i.e Perl expressions. Default: (any)
  -r <a>, --sudo <yes|no>        Toggle the use of 'sudo' when invoking 'dd'. This option has no effect if dd-paranoia is being run as root. Default: yes
  -t <s>, --block-size <size     Set the blocksize used by 'dd' to <size>. Defualt: 8M
  -l,     --ls                   List devices and exit (akin to lsblk).
  -D,     --dry-run              Take no action (disable gunzip, dd and umount). Default: no
```

## Requirements

 * `dd` (core-utils) and `xargs` (find-utils)
 * The usual suspects (`bash`, `awk`, `sed`, `grep`, `stat` and so on)

## Contact

You can reach me via github: [https://github.com/gammy](https://github.com/gammy)

