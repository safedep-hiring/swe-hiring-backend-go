# CLI Filter Tool – Coding Assignment

## Overview

The goal of this assignment is to implement a **command-line tool** (CLI) in Go that can filter entries from a **JSON array of objects** based on user-provided criteria. You are free to structure your code in a way that best demonstrates your software engineering skills, focusing on clarity, maintainability, and testability.&#x20;

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

1. **Project Structure**: Organize the code into meaningful packages or directories that reflect separation of concerns (e.g., a package or module for parsing input, a package for filter logic, and so on).
2. **Input**:
   - The CLI **must** support reading JSON from either:
     - Standard input (stdin), or
     - A file specified by a flag like `--input-file`.
   - You only need to handle valid JSON arrays of objects. You can assume the data comes in the correct format.
3. **Filtering Logic**:
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
4. **Output**:
   - The CLI prints the filtered JSON array to **standard output** in a valid JSON format.
   - If no objects match the filters, the output should be an empty array `[]`.
5. **Testing**:
   - Include **unit tests** for:
     - Filter parsing
     - Filtering logic for various operators
   - Consider adding **integration tests** or acceptance tests for the CLI if time permits.
6. **Documentation**:
   - This `README.md` (the one you’re creating) should contain a clear description of how the tool works, including:
     - **Installation** instructions
     - **Usage** examples
     - Any known **limitations** or edge cases
   - Include in-code documentation (GoDoc comments) for any public functions or types.
7. **Deliverables**:
   - A GitHub repository (or link to your solution) containing:
     1. The source code for the CLI tool.
     2. A `go.mod` file (if you are using Go modules).
     3. A suite of tests demonstrating coverage of the filter logic.
     4. This `README.md` file.
8. **Implementation Notes**:
   - We value **clarity**, **maintainability**, and **testability** over the sheer number of features.
   - You can use standard libraries or any open-source libraries that simplify parsing or argument handling.
   - Keep the code as minimal as possible while meeting the requirements and best practices.

## Example Commands

Below are some example commands and their expected outputs.

1. **Single Filter**

   ```bash
   echo '[{"id":1,"name":"Alice"},{"id":2,"name":"Bob"}]' | myfiltercli --filter "id=1"
   ```

   **Output**:

   ```json
   [
     {"id":1,"name":"Alice"}
   ]
   ```

2. **Multiple Filters**

   ```bash
   echo '[{"price":10,"type":"shirt"},{"price":20,"type":"shirt"},{"price":10,"type":"pants"}]' | myfiltercli --filter "type=shirt" --filter "price<15"
   ```

   **Output**:

   ```json
   [
     {"price":10,"type":"shirt"}
   ]
   ```

3. **Using a File Input**

   ```bash
   myfiltercli --input-file data.json --filter "category=book"
   ```

   **Output** (only items in `data.json` whose `category` is `book`).



