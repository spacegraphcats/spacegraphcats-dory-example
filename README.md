# spacegraphcats-dory-example

[![Build Status](https://travis-ci.org/spacegraphcats/spacegraphcats-dory-example.svg?branch=master)](https://travis-ci.org/spacegraphcats/spacegraphcats-dory-example)

This is an example
[spacegraphcats](https://github.com/spacegraphcats/spacegraphcats/)
project using some sequences from a Doryteuthis RNAseq assembly to
demonstrate the basic workflow.

## Quickstart

Follow the [spacegraphcats install instructions for conda](https://github.com/spacegraphcats/spacegraphcats/blob/master/doc/installing-spacegraphcats.md).

Then,

```
git clone https://github.com/spacegraphcats/spacegraphcats-dory-example
cd spacegraphcats-dory-example/
```

and now you can run the spacegraphcats workflow specified in `config.yaml`:

```
spacegraphcats run config.yaml extract_reads
```

## A brief manifest of the input files

* `./data/dory-subset.fa` - the data used to make the graph (e.g. reads or assembly)
* `./query/dory-head.fa` - query sequences
* `config.yaml` - a YAML config file that provides settings etc.

## Output files

### the `dory/` directory

This is the cDBG build directory.

* `bcalm.dory.k21.unitigs.fa` - compact De Bruijn graph (cDBG) of `dory-subset.fa` built by BCALM.
* `bcalm.dory.k21.unitigs.fa.log.txt` - BCALM build log.
* `bcalm.dory.k21.unitigs.fa.sig` - a sourmash signature of the cDBG.
* `dory.reads.bgz` - BGZF file of input reads.

### the `dory_k21_r1/` directory

This contains the info necessary to do graph queries etc. Building this
is generally the most time consuming.

The directory name is constructed from the parameters in the
`config.yaml` file.

* `cdbg.gxt` - cDBG structure.
* `commands.log` - an (incomplete) log of executed commands.
* `contigs.fa.gz` - a (potentially cleaned up) collection of cDBG contigs.
* `contigs.fa.gz.indices` - something something database something.
* `contigs.fa.gz.info.csv` - summary information for each cDBG node.
* `contigs.fa.gz.mphf` - Minimal Perfect Hash Function database for `contigs.fa.gz`.
* `contigs.fa.gz.sig` - a sourmash signature of the contigs, post processing.
* `first_doms.txt` - dominating set.
* `catlas.csv` - the catlas.
* `reads.bgz.labels` - labeled reads for fast retrieval.

### the `dory_k21_r1_search_oh0/` directory

This contains the output of the search.

* `command.txt` - an (incomplete) log of executed commands.
* `dory-head.fa.cdbg_ids.reads.fa.gz` - all of the input sequences in the neighborhood of this query; THIS IS THE MOST INTERESTING FILE :)
* `dory-head.fa.cdbg_ids.txt.gz` - list of cDBG nodes.
* `dory-head.fa.contigs.sig` - sourmash signature of output.
* `dory-head.fa.frontier.txt.gz` - list of frontier nodes (catlas).
* `dory-head.fa.response.txt` - response curve.
* `results.csv` - summary of results from all searches.
