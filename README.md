# Sunbeam's Kraken, using a locally-stashed database

This [Sunbeam] extension will stash a copy of a Kraken 1 database to a
specified location, keep that copy cached in memory with [vmtouch], and run
Sunbeam's kraken rules using the stashed database.  vmtouch isn't currently in
the common conda channels as far as I can see, so this currently requires a
vmtouch executable on your PATH.

I've found this to be necessary on one particularly strange filesystem
([IBM Spectrum Scale]) due to the [GPFS pagepool] configuration.
This should *not* be needed on either NFS or any common local filesystem, since
[the ordinary caching in Linux](https://www.linuxatemyram.com/) works as
expected for those.

[vmtouch]: https://hoytech.com/vmtouch
[Sunbeam]: https://www.sunbeam-labs.org
[IBM Spectrum Scale]: https://en.wikipedia.org/wiki/IBM_Spectrum_Scale
[GPFS pagepool]: https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/General%20Parallel%20File%20System%20(GPFS)/page/Tuning%20Parameters?section=pagepool
