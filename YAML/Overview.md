YAML (YAML Ain’t Markup Language) is a human-readable data serialization format, designed to be easy to write and understand. It’s widely used for configuration files, data exchange, and is a staple in DevOps tooling (Kubernetes, Ansible, Docker Compose, CI/CD pipelines, etc.)

# Basic Syntax and Formatting

YAML’s syntax is defined by a few simple rules:

Indentation: Use spaces (not tabs) to denote nesting. Two spaces per level is common. For example, the keys under person: are indented to show they belong to that mapping.
Key–Value Pairs: Write mappings as key: value. Keys are usually alphanumeric (use quotes only if needed).
Lists: Start list items with a hyphen (-). Each - begins a new element in the sequence.
Comments: Precede comments with #. Anything on a line after # is ignored by YAML parsers.

```bash
# Basic YAML example
Book:
  name: Unstoppable
  author: Sk-publication
  language:
    - English
    - Hindi
```
# Core Data Types
YAML natively supports several core data types:

Scalars: These include strings, integers, floats, booleans, and nulls. YAML usually auto-detects types:

Strings: Plain (unquoted) strings (e.g. title: Hello), or quoted with " or ' for special characters. Escape sequences (like \n) work in double-quoted strings.
Numbers: Integers (age: 42) and floats (pi: 3.14159) are written without quotes.
Booleans: Represented as true/false (lowercase).
Null: Use null or ~ to denote a null value.
Sequences (Lists): Ordered collections denoted by - entries. E.g.:

```bash
#Sample Code
app:
  name: MyApp
  version: 1.0
  active: true
  description: "A sample YAML file"
  nullable_field: ~
  tags:
    - backend
    - production
  limits:
    cpu: 2
    memory: 512
```
# Some Feature:
## 1. Anchors (&) and Aliases (*) — Reuse Code Without Rewriting
YAML lets you reuse parts of your configuration to avoid repeating the same data again and again.To keep your YAML file DRY (Don’t Repeat Yourself). It makes it cleaner and easier to maintain.

```bash
defaults: &default_settings
  retries: 3
  timeout: 30

service1:
  <<: *default_settings
  host: example.com
```
&default_settings: This creates a named block (anchor) called default_settings.

*default_settings: This reuses that block wherever you want.

<<: *default_settings: This merges the settings into service1.

## 2. Multi-line Strings — Write Big Text Blocks
If you need to add large texts (like logs, descriptions, or messages), YAML supports it using two ways:

a) Literal Style (|) – Keeps new lines
```bash
note: |
  This is a multiline
  string in literal style.
```
b) Folded Style (>) – Joins lines with spaces
```bash
summary: >
  This is a folded
  style multiline string.
```
Output becomes:
This is a folded style multiline string.
