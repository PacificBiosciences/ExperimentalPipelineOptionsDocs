# HGAP Options
## Usage
Copy/paste these into the Advanced textbox for your pipeline.
Modify as desired.

## Common details
These are all in JSON format. Whitespace is ignored (except within quotes).

The `"hgap"` section can be used to auto-generate defaults for the other sections.
(Default-generation can be suppressed with `hgap/SuppressAuto: true`.)
The other sections then override any defaults.

We ignore the case of all keys. (The underscores are needed, for historical reasons.)
We also ignore any keys with leading or trailing underscores, so those can be used
for comments.

Note that all values are strings. That avoids problems like integer size limitations
and exact case of True/False.

We recommend that you copy these into a JSON format-checker before modifying. We
use a fairly strict JSON parser.

## Descriptions of options
(This section will be moved to another page, probably.)

```js
{
  "hgap": {
    "SuppressAuto_bool_": "If not false, 0, nor empty, suppress the auto-generation of values (e.g. length_cutoff).",
    "GenomeSize_int_": "If not 0 nor empty, substitute internal defaults for all options (before overrides).",
    "min_length_cutoff_int_": "If provided, then falcon/length_cutoff will be raised to this if lower.",
    "_comment": "Overrides for full HGAP pipeline"
  },
  "falcon": {
    "_comment": "Overrides for FALCON"
  },
  "pbalign": {
    "_comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "_comment": "Overrides for genomic consensus (polishing)"
  },
  "pbsmrtpipe": {
    "_comment": "Overrides for pbsmrtpipe"
  },
  "_comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
}
```

## Minimal options
This is enough.
```js
{
  "hgap": {
    "GenomeSize": "10000000",
    "min_length_cutoff": "500"
  }
}
```
The rest would be auto-generated for you.

## Defaults
These (probably) correspond to out internal defaults.
If you want to set any or all options explicitly, copy/paste into the textbox
for your pipeline stage, and modify as desired.

### Common defaults
If you provide nothing, you'll have these defaults. Also, if you do not override these, then you will still have these.

(This needs to be updated.)

```js
{
  "hgap": {
    "SuppressAuto": true,
    "GenomeSize": 8000,
    "min_length_cutoff": 1,
    "~comment": "Overrides for full HGAP pipeline"
  },
  "falcon": {
    "falcon_sense_option": "--output_multi --min_idt 0.77 --min_cov 10 --max_n_read 2000 --n_core 6",
    "length_cutoff": "1200",
    "length_cutoff_pr": "50",
    "overlap_filtering_setting": "--max_diff 1000 --max_cov 100000 --min_cov 0 --bestn 1000 --n_core 4",
    "ovlp_DBsplit_option": "-s50 -a",
    "ovlp_HPCdaligner_option": "-v -k15 -h60 -w6 -e.95 -l40 -s100 -M16",
    "ovlp_concurrent_jobs": "32",
    "pa_DBsplit_option": "-x1200 -s500 -a",
    "pa_HPCdaligner_option": "-v -k16 -h35 -w7 -e.70 -l40 -s100 -M16",
    "pa_concurrent_jobs": "32",
    "~comment": "Overrides for FALCON"
  },
  "pbalign": {
    "options": "--hitPolicy randombest --minAccuracy 70.0 --minLength 50 --algorithm=blasr",
    "algorithmOptions": "-minMatch 12 -bestn 10 -minPctSimilarity 70.0",
    "_jdnotes": "--maxHits 1 --minAnchorSize 12 --maxDivergence=30 --minAccuracy=0.75 --minLength=50 --hitPolicy=random --seed=1",
    "~comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "options": "--algorithm arrow --minConfidence 40 --minCoverage 5",
    "~comment": "Overrides for genomic consensus (polishing)"
  },
  "pbcoretools.tasks.filterdataset": {
    "other_filters": "rq >= 0.7",
    "read_length": 0
  },
  "pbsmrtpipe": {
    "~comment": "Overrides for pbsmrtpipe"
  },
  "~comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
}
```

### Lambda
```js
{
  "hgap": {
    "SuppressAuto": true,
    "GenomeSize": 8000,
    "min_length_cutoff": 1,
    "_comment": "Overrides for full HGAP pipeline"
  },
  "falcon": {
    "falcon_sense_option": "--output_multi --min_idt 0.77 --min_cov 10 --max_n_read 2000 --n_core 6",
    "length_cutoff": "1200",
    "length_cutoff_pr": "50",
    "overlap_filtering_setting": "--max_diff 1000 --max_cov 100000 --min_cov 0 --bestn 1000 --n_core 4",
    "ovlp_DBsplit_option": "-s50 -a",
    "ovlp_HPCdaligner_option": "-v -k15 -h60 -w6 -e.95 -l40 -s100 -M16",
    "ovlp_concurrent_jobs": "32",
    "pa_DBsplit_option": "-x1200 -s500 -a",
    "pa_HPCdaligner_option": "-v -k16 -h35 -w7 -e.70 -l40 -s100 -M16",
    "pa_concurrent_jobs": "32",
    "_comment": "Overrides for FALCON"
  },
  "pbalign": {
    "_comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "_comment": "Overrides for genomic consensus (polishing)"
  },
  "pbsmrtpipe": {
    "_comment": "Overrides for pbsmrtpipe"
  },
  "_comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
}
```

### Generic
These are minimal settings. You can use these to let the tool generate its own defaults.

Comments can be removed. But note that strict JSON disallows trailing commas
for the final field of any dictionary section.
```js
{
  "hgap": {
    "SuppressAuto": "false",
    "GenomeSize": "10000000",
    "min_length_cutoff": "500",
    "_comment": "Overrides for full HGAP pipeline"
  },
  "falcon": {
    "_comment": "Overrides for FALCON"
  },
  "pbalign": {
    "_comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "_comment": "Overrides for genomic consensus (polishing)"
  },
  "pbsmrtpipe": {
    "_comment": "Overrides for pbsmrtpipe"
  },
  "_comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
}
```

### Empty
(This section is only for starting new sections.)
```js
{
  "hgap": {
  },
  "falcon": {
    "_comment": "Overrides for FALCON"
  },
  "pbalign": {
    "_comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "_comment": "Overrides for genomic consensus (polishing)"
  },
  "pbsmrtpipe": {
    "_comment": "Overrides for pbsmrtpipe"
  },
  "_comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
}
```
