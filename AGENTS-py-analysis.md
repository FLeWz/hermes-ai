# Agent Instructions

This file contains project-specific development and data-handling instructions.

## Project Development

- Default language: Python.
- Exploration is allowed when necessary to understand the inputs or answer the requested task.

## File-Based Datasets

For CSV and other tabular files:

- inspect the original file directly;
- pass the original file path to the implementation;
- run the implementation directly against the original file;
- never copy the dataset for verification.

## SQLite

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
