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

For me, this takes ~6 seconds.

To determine time spent validating the samplesheet.

```bash
$ grep 'Starting validation' -A1 .nextflow.log

Sep-06 10:43:29.713 [main] DEBUG nextflow.validation.SchemaValidator - Starting validation: 'input': '/apetkau/from-samplesheet-test-nf/main/samplesheet.pe.30.csv' with 'assets/schema_input.json'
Sep-06 10:43:29.878 [main] DEBUG nextflow.validation.SchemaValidator - Validation passed: 'input': '/apetkau/from-samplesheet-test-nf/main/samplesheet.pe.30.csv' with 'assets/schema_input.json'
--
Sep-06 10:43:29.903 [main] DEBUG nextflow.validation.SchemaValidator - Starting validation: '/apetkau/from-samplesheet-test-nf/main/samplesheet.pe.30.csv' with 'assets/schema_input.json'
Sep-06 10:43:29.952 [main] DEBUG nextflow.validation.SchemaValidator - Validation passed: '/apetkau/from-samplesheet-test-nf/main/samplesheet.pe.30.csv' with 'assets/schema_input.json'
```

That is it takes < 1 second for validation, however, this is repeated twice.

Or, in summary:
* **Total runtime**: 6 seconds
* **Validation time**: < 1 second (x2)

### Case: 60 paired-end samples

Repeating above with the file <https://raw.githubusercontent.com/apetkau/from-samplesheet-test-nf/main/samplesheet.pe.60.csv> gives:

* **Total runtime**: 6 seconds
* **Validation time**: < 1 second (x2)

## Single-end

Compare the above run-times to the single-end cases.

### Case: 30 single-end samples

```bash
time nextflow run apetkau/from-samplesheet-test-nf -r main --input https://raw.githubusercontent.com/apetkau/from-samplesheet-test-nf/main/samplesheet.se.30.csv
```

```
$ grep 'Starting validation' -A1 .nextflow.log

Sep-06 10:45:47.894 [main] DEBUG nextflow.validation.SchemaValidator - Starting validation: 'input': '/apetkau/from-samplesheet-test-nf/main/samplesheet.se.30.csv' with 'assets/schema_input.json'
Sep-06 10:46:11.016 [main] DEBUG nextflow.validation.SchemaValidator - Validation passed: 'input': '/apetkau/from-samplesheet-test-nf/main/samplesheet.se.30.csv' with 'assets/schema_input.json'
--
Sep-06 10:46:11.035 [main] DEBUG nextflow.validation.SchemaValidator - Starting validation: '/apetkau/from-samplesheet-test-nf/main/samplesheet.se.30.csv' with 'assets/schema_input.json'
Sep-06 10:46:34.027 [main] DEBUG nextflow.validation.SchemaValidator - Validation passed: '/apetkau/from-samplesheet-test-nf/main/samplesheet.se.30.csv' with 'assets/schema_input.json'
```

Summary:
* **Total runtime**: 52 seconds
* **Validationt time**: 24 + 13 seconds

### Case: 60 single-end samples

Use <https://raw.githubusercontent.com/apetkau/from-samplesheet-test-nf/main/samplesheet.se.60.csv>.

* **Total runtime**: 12 minutes 14 seconds (734 seconds)
* **Validation time**: 368 + 360 seconds 
