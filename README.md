# CLI Filter Tool – Coding Assignment

## Overview

The goal of this assignment is to implement a **command-line tool** (CLI) in Go that can filter entries from a **JSON array of objects** based on user-provided criteria. You are free to structure your code in a way that best demonstrates your software engineering skills, focusing on clarity, maintainability, and testability.

- [CLI Filter Tool – Coding Assignment](#cli-filter-tool--coding-assignment)
  - [Overview](#overview)
  - [Description](#description)
    - [Example](#example)
  - [Requirements](#requirements)
    - [Project Structure](#project-structure)
    - [Input](#input)
    - [Filtering Logic](#filtering-logic)
    - [Output](#output)
    - [Testing](#testing)
    - [Documentation](#documentation)
    - [Deliverables](#deliverables)
    - [Implementation Notes](#implementation-notes)
  - [Example Commands](#example-commands)
    - [Single Filter](#single-filter)
    - [Multiple Filters](#multiple-filters)
    - [Using a File Input](#using-a-file-input)
  - [Submission](#submission)

## Description

A user will run a CLI that reads a JSON array either from:

1. **Standard input (stdin)**, or
2. An **input file** (provided via a command-line flag, e.g. `--input-file`)

The CLI then filters the JSON array based on one or more **filter conditions** specified via the command line, and writes the filtered JSON array to **standard output**.

### Example

Suppose you have the following JSON data:

```json
[
  {"id": 1, "category": "book", "price": 12.99},
  {"id": 2, "category": "electronics", "price": 299.99},
  {"id": 3, "category": "book", "price": 9.99},
  {"id": 4, "category": "stationery", "price": 1.99},
  {"id": 5, "category": "book", "price": 20.00}
]
```

A user might run:

```bash
cat data.json | myfiltercli --filter "category=book" --filter "price<15"
```

In this scenario, the CLI would parse the array, filter out objects that **do not** have `category = book` or `price < 15`, and output the resulting JSON:

```json
[
  {"id": 1, "category": "book", "price": 12.99},
  {"id": 3, "category": "book", "price": 9.99}
]
```

## Requirements

### Project Structure
Organize the code into meaningful packages or directories that reflect separation of concerns and your own preferences.

### Input
- The CLI **must** support reading JSON from either:
  - Standard input (stdin), or
  - A file specified by a flag like `--input-file`.
- You only need to handle valid JSON arrays of objects. Fail fast if the input is not a valid JSON array.

### Filtering Logic
- Users can specify one or more filters via command-line flags (e.g., `--filter "<expression>"`).
- **Examples** of valid expressions:
  - `"price<10"`
  - `"category=book"`
  - `"id>3"`
- The CLI should parse these expressions, apply them to each object in the JSON array, and only **keep** objects that match **all** provided filter expressions.
- You only need to handle comparisons of the form **`=`**, **`<`**, **`>`**, **`<=`**, **`>=`**, and **`!=`**.
- Assume filters only apply to top-level fields (no nested objects) and that these fields can be:
  - **Numbers**: interpret them as float or int.
  - **Strings**: interpret them as case-sensitive string comparisons.

### Output
- The CLI prints the filtered JSON array to **standard output** in a valid JSON format.
- If no objects match the filters, the output should be an empty array `[]`.

### Testing
- Include **unit tests** for:
  - Filter parsing
  - Filtering logic for various operators
- Consider adding **integration tests** or acceptance tests for the CLI if time permits

### Documentation
- This `README.md` (the one you're creating) should contain a clear description of how the tool works, including:
  - **Installation** instructions
  - **Usage** examples
  - Any known **limitations** or edge cases
- Include in-code documentation (GoDoc comments) for any public functions or types
- Create a `CONTRIBUTING.md` file that outlines the process for contributing to the project

### Deliverables
A GitHub repository containing:

1. The source code for the CLI tool and any supporting files
2. This `README.md` file
3. A `CONTRIBUTING.md` file that outlines the process for contributing to the project

### Implementation Notes
- Prefer **clarity**, **maintainability**, and **testability** over the sheer number of features.
- You can use standard libraries or any open-source libraries that simplify parsing or argument handling
- Keep the code as minimal as possible while meeting the requirements and best practices

## Example Commands

Below are some example commands and their expected outputs.

### Single Filter

```bash
echo '[{"id":1,"name":"Alice"},{"id":2,"name":"Bob"}]' | myfiltercli --filter "id=1"
```

**Output**:

```json
[
  {"id":1,"name":"Alice"}
]
```

### Multiple Filters

```bash
echo '[{"price":10,"type":"shirt"},{"price":20,"type":"shirt"},{"price":10,"type":"pants"}]' | myfiltercli --filter "type=shirt" --filter "price<15"
```

**Output**:

```json
[
  {"price":10,"type":"shirt"}
]
```

### Using a File Input

```bash
myfiltercli --input-file data.json --filter "category=book"
```

**Output** (only items in `data.json` whose `category` is `book`).

## Submission

1. Create a [private fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) of this repository.
2. Commit your code to the forked repository's `dev` branch
3. Create a pull request from your `dev` branch to the `main` branch in your private fork
4. Invite [@abhisek](https://github.com/abhisek) to your private fork repository
5. Add `@abhisek` as a reviewer to the pull request
