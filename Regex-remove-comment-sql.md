Removing comments from SQL queries involves targeting both single-line and multi-line comments. SQL single-line comments start with `--`, and multi-line comments are enclosed between `/*` and `*/`.

### Regex Patterns

1. **Single-line Comments**: For single-line comments that start with `--` and go until the end of the line, you can use:
   ```
   --.*(\n|$)
   ```
   This pattern matches anything that starts with `--` and captures all characters until the end of the line or the document.

2. **Multi-line Comments**: For multi-line comments that start with `/*` and end with `*/`, you can use:
   ```
   /\*[\s\S]*?\*/
   ```
   This pattern matches anything that starts with `/*`, followed by any character (including new lines, which is what `[\s\S]*?` captures), until it finds the closing `*/`.

### Combined Pattern

To remove both types of comments with a single regex operation, you can combine these patterns using the `|` operator, which acts as an OR. Here's how the combined regex looks:
```
--.*(\n|$)|/\*[\s\S]*?\*/
```
This pattern will match and allow you to replace both single-line and multi-line comments in a SQL file.

### Implementation Note

When using regex to modify code or queries, it's essential to be cautious and test the changes on a copy of your data first. Regex can have unintended matches that could alter or remove parts of the SQL query itself if the patterns are not precise enough or if the SQL contains strings that might inadvertently match these patterns.

### Practical Usage

In many programming languages or tools that support regex, you can use this pattern in a search and replace functionality, where you search for the pattern and replace it with an empty string to remove the comments.

Here's a quick example in Python:

```python
import re

sql_code = """SELECT * FROM users; -- This is a single-line comment
/*
This is a multi-line comment
*/
SELECT * FROM products;"""

# Removing both single-line and multi-line comments
cleaned_sql = re.sub(r'--.*(\n|$)|/\*[\s\S]*?\*/', '', sql_code)

print(cleaned_sql.strip())
```

This script will print the SQL code without the comments. Remember, the effectiveness of regex can depend on the specifics of the SQL code and the regex engine being used.
