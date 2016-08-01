# HGAP Options
In the smrtlink UI, when using the "Assembly (HGAP 5)" *Analysis Application*,
you can click "ADVANCED ANALYSIS PARAMETERS" to see a pop-up with 4 textboxes.
Three of those are the basic levers available, whenever defaults suffice.

However, if you need to override any of the defaults, you may paste a JSON
value into the 4th textbox, called "Experimental HGAP.5 config overrides."

This page documents all settings available as overrides in that box.

## Usage
Copy/paste these into the "Experimental HGAP.5 config overrides" textbox
within the "Advanced Analysis Parameters" pop-up for your HGAP5 pipeline.
Modify as desired. These will override any other settings provided via the
web UI.

## Common details
These are all in JSON format. Whitespace is ignored (except within quotes).

The `"hgap"` section can be used to auto-generate defaults for the other sections.
(Default-generation can be suppressed with `hgap/SuppressAuto: true`.)
The other sections then override any defaults.

We ignore the case of all keys. (The underscores are needed, for historical reasons.)
We also ignore any keys with leading or trailing tildes, so those can be used
for comments.

Note that all values are **strings**. That avoids problems like integer-size limitations
and the exact case of True/False. However, any proper JSON values are accepted and
converted to strings.

## Descriptions of options
Each section applies to a different tool (which is why they follow different conventions).
The "hgap" section applies to the workflow itself. The "pbsmrtpipe" applies to that portion
of the workflow, in case you know something about the internals.

```js
{
  "hgap": {
    "SuppressAuto": "If not false, 0, nor empty, suppress the auto-generation of values (e.g. length_cutoff).",
    "min_length_cutoff": "If provided, then falcon/length_cutoff will be raised to this if lower.",
    "~comment": "Overrides for full HGAP pipeline"
  },
  "falcon": {
    "~comment": "Overrides for FALCON"
  },
  "pbalign": {
    "~comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "~comment": "Overrides for genomic consensus (polishing)"
  },
  "pbsmrtpipe": {
    "~comment": "Overrides for pbsmrtpipe"
  },
  "~comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
}
```

## Minimal options
This is enough.
```js
{
  "falcon": {
    "genome_size": "10000000",
    "seed_coverage": "30",
    "length_cutoff": "-1",
  }
}
```
The rest would be auto-generated for you.

### UI options
Via the UI, you do not even need those minimal options since you can provide these values via
"Advanced Analysis Parameters", which is equivalent to setting this:
```js
{
  "hgap": {
    "HGAP_GenomeLength_str": "10000000",
    "HGAP_SeedCoverage_str": "30",
    "HGAP_SeedLengthCutoff_str": "-1",
  }
}
```
In other words, UI options map directly to `"hgap"` options with `HGAP_*` prefixes,
and those are used to generate other options. But anything provided directly in
the "Experimental HGAP.5 config overrides" textarea of the UI will override all
the other UI textareas.

## Available options and default values
These (probably) correspond to our internal defaults.
If you want to set any or all options explicitly, copy/paste into the textbox
for your pipeline stage, and modify as desired.

### Common defaults
If you provide nothing, you will have these defaults. Also, if you do not override these, then you will still have these.

(This needs to be updated.)

```js
{
  "hgap": {
    "SuppressAuto": "false",
    "min_length_cutoff": "500",
    "~comment": "Overrides for full HGAP pipeline"
  },
  "falcon": {
    "genome_size": "REQUIRED",
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
    "seed_coverage": "30",
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
    "min_length_cutoff": 1,
    "~comment": "Overrides for full HGAP pipeline"
  },
  "falcon": {
    "genome_size": "8000",
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
    "~comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "~comment": "Overrides for genomic consensus (polishing)"
  },
  "pbsmrtpipe": {
    "~comment": "Overrides for pbsmrtpipe"
  },
  "~comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
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
    "min_length_cutoff": "500",
    "~comment": "Overrides for full HGAP pipeline"
  },
  "falcon": {
    "genome_size": "10000000",
    "~comment": "Overrides for FALCON"
  },
  "pbalign": {
    "~comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "~comment": "Overrides for genomic consensus (polishing)"
  },
  "pbsmrtpipe": {
    "~comment": "Overrides for pbsmrtpipe"
  },
  "~comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
}
```

### Empty
(This section is only for starting new sections.)
```js
{
  "hgap": {
  },
  "falcon": {
    "~comment": "Overrides for FALCON"
  },
  "pbalign": {
    "~comment": "Overrides for blasr alignment (prior to polishing)"
  },
  "variantCaller": {
    "~comment": "Overrides for genomic consensus (polishing)"
  },
  "pbsmrtpipe": {
    "~comment": "Overrides for pbsmrtpipe"
  },
  "~comment": "https://github.com/PacificBiosciences/ExperimentalPipelineOptionsDocs/HGAP"
}
```
