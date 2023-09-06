# Repostiory for testing fromSamplesheet

This repository is used to test out fromSamplesheet with paired/single-end fastq data for comparing running times.

In order to run, first do `nextflow pull` to download the pipeline files:

```bash
nextflow pull apetkau/from-samplesheet-test-nf
```

Now, you can follow the below instructions to test out different cases.

## Paired-end

### Case: 30 paired-end samples

To extract running times for paired-end data:

```bash
time nextflow run apetkau/from-samplesheet-test-nf -r main --input https://raw.githubusercontent.com/apetkau/from-samplesheet-test-nf/main/samplesheet.pe.30.csv
```

For me, this takes ~5 seconds.

To determine time spent validating the samplesheet.

```bash
$ grep 'Starting validation' -A1 .nextflow.log
Aug-30 12:17:15.572 [main] DEBUG nextflow.validation.SchemaValidator - Starting validation: 'samplesheet.pe.30.csv' with 'assets/schema_input.json'
Aug-30 12:17:16.074 [main] DEBUG nextflow.validation.SchemaValidator - Validation passed: 'samplesheet.pe.30.csv' with `assets/schema_input.json'
```

That is it takes < 1 second for validation.

Or, in summary:
* **Total runtime**: 5 seconds
* **Validation time**: < 1 second

### Case: 60 paired-end samples

Repeating above with the file <https://raw.githubusercontent.com/apetkau/from-samplesheet-test-nf/main/samplesheet.pe.60.csv> gives:

* **Total runtime**: 6 seconds
* **Validation time**: < 1 second

## Single-end

Compare the above run-times to the single-end cases.

### Case: 30 single-end samples

```bash
time nextflow run apetkau/from-samplesheet-test-nf -r main --input https://raw.githubusercontent.com/apetkau/from-samplesheet-test-nf/main/samplesheet.se.30.csv
```

```
$ grep 'Starting validation' -A1 .nextflow.log
Aug-30 12:25:06.349 [main] DEBUG nextflow.validation.SchemaValidator - Starting validation: 'samplesheet.se.30.csv' with 'assets/schema_input.json'
Aug-30 12:25:31.110 [main] DEBUG nextflow.validation.SchemaValidator - Validation passed: 'samplesheet.se.30.csv' with `assets/schema_input.json'
```

Summary:
* **Total runtime**: 30 seconds
* **Validationt time**: 25 seconds

### Case: 60 single-end samples

Use <https://raw.githubusercontent.com/apetkau/from-samplesheet-test-nf/main/samplesheet.se.60.csv>.

* **Total runtime**: 6 minutes 27 seconds (387 seconds)
* **Validation time**: 382 seconds 
