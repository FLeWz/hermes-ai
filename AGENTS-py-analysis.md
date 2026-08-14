# Agent Instructions

This file contains project-specific development and data-handling instructions.

Global engineering, communication, and Git policies are defined by the global
Hermes `SOUL.md` and apply in addition to these instructions.

## Project Development

- Write reliable, executable code.
- Default language: Python.
- Prefer simple, transparent implementations over unnecessary frameworks.
- When existing code is present, treat it as the source of truth.
- Inspect existing code before modifying it.
- Make the smallest change that satisfies the request.
- Patch existing files in place rather than creating parallel replacements.
- Preserve unrelated existing behavior.
- Only create a new implementation when no suitable existing implementation
  exists or the user explicitly requests an independent implementation.

## Input Inspection

Before substantial analysis or code changes, inspect the actual inputs.

Identify:

- input files or databases;
- relevant schemas and structures;
- column names and data types;
- representative records;
- missing values;
- likely identifiers;
- obvious duplicate records;
- relevant dimensions such as row and column counts.

Never assume filenames, column names, types, identifiers, or relationships are
correct without inspection.

If the available data is insufficient to perform the requested task reliably,
say so rather than inventing assumptions.

## Analysis Integrity

Clearly distinguish:

- **Observed** — facts directly obtained from the input.
- **Calculated** — values computed from the input.
- **Interpreted** — conclusions derived from observed or calculated results.
- **Assumed** — information not established by the input.

Never present an assumption, calculation, or interpretation as an observed fact.

If an assumption materially affects the result, state it explicitly.

## Source Data Protection

The original input dataset is the canonical source and must remain unchanged
unless the user explicitly requests mutation.

Do not:

- overwrite source files;
- delete or update source records;
- alter source schemas;
- transform source datasets in place;
- write generated analysis results into source datasets.

Read and execute against the original source directly.

Generated outputs must be written to the designated output location.

## No-Temporary-Data Policy

Unless the user explicitly requests temporary copies or isolated testing, do
not create:

- `/tmp`;
- `tmp/`;
- `scratch/`;
- staging directories;
- copied datasets;
- temporary script copies;
- throwaway verification scripts;
- ad-hoc verification programs;
- parallel implementations used only for verification.

The original dataset is the canonical development and verification dataset.

Use this workflow:

    ORIGINAL INPUT
          ↓
    INSPECT INPUT
          ↓
    INSPECT EXISTING CODE
          ↓
    PATCH EXISTING CODE
          ↓
    RUN PATCHED CODE AGAINST ORIGINAL INPUT
          ↓
    INSPECT REAL OUTPUT / ERRORS / WARNINGS
          ↓
    PATCH AGAIN IF NECESSARY
          ↓
    RUN AGAIN AGAINST ORIGINAL INPUT

Do not introduce an intermediate dataset, temporary script, or separate
verification implementation.

## Execution and Verification

After creating or modifying code:

1. Run the actual implementation.
2. Run it directly against the original input when applicable.
3. Inspect:
   - execution errors;
   - warnings;
   - stdout/stderr;
   - generated files;
   - relevant output values;
   - relevant visualizations or artifacts.
4. Determine whether errors or warnings affect correctness.
5. Fix issues that affect correctness.
6. Re-run the actual implementation.
7. Repeat only as necessary.

A file that has not actually been executed must not be described as tested or
verified.

Do not create separate verification code merely to demonstrate correctness.

Do not perform unrelated ad-hoc analysis merely to demonstrate correctness
when execution of the actual implementation provides the required verification.

## File-Based Datasets

For CSV and other tabular files:

- inspect the original file directly;
- pass the original file path to the implementation;
- run the implementation directly against the original file;
- never copy the dataset for verification.

## SQLite

For SQLite:

- inspect the original database directly;
- inspect tables, columns, indexes, and row counts;
- inspect likely primary keys;
- inspect relevant missing values;
- inspect representative records;
- use read-only connections when analysis does not require mutation;
- run analysis queries against the original database.

Use SQL for operations naturally expressed in SQL, including:

- filtering;
- joining;
- aggregation;
- grouping;
- counting;
- sorting;
- duplicate detection;
- missing-value checks;
- schema inspection.

Do not copy the database to a temporary location for verification.

## Exploratory Analysis

Exploration is allowed when necessary to understand the inputs or answer the
requested task.

However:

- do not create unnecessary exploratory scripts;
- do not create scratch datasets;
- do not copy source files;
- do not perform unrelated analysis;
- reuse the actual implementation when practical;
- prefer direct inspection, SQL queries, or appropriate standard tools.

Exploration must support the requested task.

## Python Standards

Python code should:

- use clear imports;
- define meaningful variables;
- avoid hidden global state;
- use functions for substantial operations;
- accept input paths explicitly;
- avoid undocumented working-directory dependencies;
- produce deterministic output where practical;
- clearly identify output paths;
- fail with useful error messages;
- preserve original input data.

Prefer straightforward Python over unnecessary abstractions or frameworks.

## Reproducibility

Save reproducible code and generated artifacts when appropriate.

Code should:

- accept explicit inputs;
- clearly identify outputs;
- preserve source data;
- avoid undocumented environment or working-directory assumptions;
- use deterministic behavior where practical;
- be executable against the actual project inputs.

Do not create a second implementation that duplicates the analysis logic merely
for verification.

## Completion Criteria

A task is complete when:

- the requested change has been implemented;
- existing code was changed minimally where applicable;
- original source data remains unchanged;
- the actual implementation has been executed;
- execution used the original input where applicable;
- relevant outputs and artifacts have been inspected;
- correctness-affecting errors have been resolved;
- remaining limitations or assumptions are clearly stated;
- the global Git policy has been followed and the completed change committed
  when applicable.

Do not claim that something was tested or verified if it was only inspected
statically.

## Project-Specific Overrides

Project-specific requirements may be added below this section.

Examples include:

- required Python version;
- dependency management;
- test commands;
- linting or formatting commands;
- build commands;
- deployment procedures;
- required output directories;
- project architecture;
- domain-specific data conventions.

These project-specific requirements supplement the global `SOUL.md` rules and
must not silently contradict them.
