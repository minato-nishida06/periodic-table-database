# Periodic Table Database

A command-line lookup tool for periodic table elements, built with Bash and PostgreSQL. Query any element by name, symbol, or atomic number and get back its type, atomic mass, melting point, and boiling point.

## How It Works

- Run the script with an element's name, symbol, or atomic number as an argument.
- The script queries a normalized PostgreSQL database (`elements`, `properties`, and `types` tables, joined together) to look up the matching element.
- If found, it prints a formatted summary including the element's type (e.g., metal, nonmetal, metalloid), atomic mass, melting point, and boiling point.
- If no argument is given, or the element isn't found, the script prints a helpful message instead of failing silently.

## Example

```bash
./element.sh Hydrogen
```
```
The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259 celsius and a boiling point of -253 celsius.
```

You can also query by symbol or atomic number:
```bash
./element.sh H
./element.sh 1
```

## Built With
- Bash
- PostgreSQL (via `psql`)

## Database Schema
The data is split across normalized tables rather than one flat table:
- `elements` — name, symbol, atomic number
- `properties` — atomic mass, melting point, boiling point, linked by atomic number
- `types` — element classification (metal, nonmetal, metalloid), joined via `type_id`

## Setup

1. Make sure PostgreSQL is installed and running.
2. Create a database named `periodic_table` and load the schema/data from `periodic_table.sql`:
   ```bash
   psql --username=freecodecamp --dbname=periodic_table -f periodic_table.sql
   ```
3. Make the script executable:
   ```bash
   chmod +x element.sh
   ```

## Usage

```bash
./element.sh <name | symbol | atomic number>
```

## What This Project Demonstrates
- Relational database design with normalized tables and foreign key relationships
- SQL `INNER JOIN` queries across multiple tables
- Bash scripting with conditional logic and argument handling
- Building a database-backed CLI tool from scratch
