# Sunbeam's Kraken, using a locally-stashed database

This [Sunbeam] extension will stash a copy of a [Kraken] 1 database to a
specified location, keep that copy cached in memory with [vmtouch], and run
Sunbeam's classification rules using the stashed database.

I've found this to be necessary on one particularly strange filesystem
([IBM Spectrum Scale]) due to the [GPFS pagepool] configuration.
This should *not* be needed on either NFS or any common local filesystem, since
[the ordinary caching in Linux](https://www.linuxatemyram.com/) works as
expected for those.

## Installation

    git clone git@github.com:ressy/sbx_kraken_stash.git sunbeam/extensions/sbx_kraken_stash
    conda install -c conda-forge --file requirements.txt
    cat sunbeam/extensions/sbx_kraken_stash/config.yml >> sunbeam_config.yml

Customize the `db_root` path in the new configuration lines as needed.  The
database files will be copied to this location within their original directory
name (as already defined in the `classify` config section).

## Running

If using with `--cluster` be sure to constrain the classify step to a single
host, or else a separate local database copy will be created across multiple
servers.

[Kraken]: https://ccb.jhu.edu/software/kraken/
[vmtouch]: https://hoytech.com/vmtouch
[Sunbeam]: https://www.sunbeam-labs.org
[IBM Spectrum Scale]: https://en.wikipedia.org/wiki/IBM_Spectrum_Scale
[GPFS pagepool]: https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/General%20Parallel%20File%20System%20(GPFS)/page/Tuning%20Parameters?section=pagepool
