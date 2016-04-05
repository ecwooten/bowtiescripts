# bowtiescripts

Git repository of scripts useful for running bowtie alignments and aggregating read counts.

## SCRIPTS

Script files are located in *lib* subdirectory. To run, execute with `node ./lib/[script_name]` or make script executable and execute with just `./lib/[script_name]`

### bowtie-counter
**run bowtie alignments against multiple sequence read files, aggregating read counts and summarizing alignments**

required arguments:
  * --fasta_file - path to fasta file to align against
  * --fastq_directory - path to directory containing fastq files for alignment (if bowtie2 is used, these files may be .gz or .bz2 archives)
  * --output_directory - path to directory to output resulting count files to
  * --summary_file - path to save a summary file to, summarizing the results of bowtie alignments

optional arguments:
  * --bowtie_cmd - command to run bowtie, must be available in PATH or resolve to bowtie binary (default: "bowtie2")
  * --bowtie_args.\[argument name (with - or -- if required)\]=\[argument value\] - arguments to be passed to bowtie command. defaults:
    * -p=\[parallel cores to use (all cores on your system)\]
    *  -x=\[path to index files\]
    *-U=\[path to fastq file\]

    * refer to documentation for bowtie options:
      * bowtie2 - <http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#command-line>
      * bowtie - <http://bowtie-bio.sourceforge.net/manual.shtml#command-line>

  * --bowtie\_build\_cmd - command to run bowtie build, must be available in PATH or resolve to bowtie binary (default: "bowtie2-build")
  * --bowtie\_build\_args.\[argument name (with - or -- if required)\]=\[argument value\] - arguments to be passed to bowtie build command. defaults:
    * -f=\[path to fasta file\]

    * refer to documentation for bowtie index build options:
      * bowtie2-build - <http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#command-line-1>
      * bowtie-build - <http://bowtie-bio.sourceforge.net/manual.shtml#command-line-1>

  * --index_file - path to save index files to (default: temp file)
  * --fastq\_file\_list - csv file of fastq files to run (optional, files will be filtered to those matching files included in this list, prefixes are permissable)
  * --remove_index - remove index files after running (default: true)
  * --output_format - format to save count and summary files, json or csv (default: csv)
  * --concurrency - number of alignments / counts to run at once (default: 1)
  * --help|h|usage - print usage
  * --verbose - print child process output (default: false)

## INSTALLATION

These scripts are currently designed to run with [Node.js](https://nodejs.org/en/), which is ideal for high-thoroughput and parallelizable disk / process IO required for bowtie alignments. The scripts make minimal use of temporary files, and pipe process output directly, speeding up the counting / aggregation process. They have been tested on Linux, but should work find on Windows and Mac sytems. Additionally, they have been tested running on up to 40 parallel CPUs on Amazon EC2 (m4.10xlarge) instances.

  * [Mac Node.js Installer](https://nodejs.org/dist/v4.4.2/node-v4.4.2.pkg)
  * [Windows Node.js Installer](https://nodejs.org/dist/v4.4.2/node-v4.4.2-x86.msi)
