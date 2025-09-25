# AIDB SQL Technical Manual

This manual provides a comprehensive overview of the SQL commands supported by the AIDB query engine.

## Data Definition Language (DDL)

DDL commands are used to define and manage the database schema.

### CREATE DATABASE

Creates a new database.

**Syntax:**

```sql
CREATE DATABASE [IF NOT EXISTS] database_name;
```

**Parameters:**

*   `IF NOT EXISTS`: If specified, the database will only be created if a database with the same name does not already exist.
*   `database_name`: The name of the new database.

### DROP DATABASE

Drops an existing database.

**Syntax:**

```sql
DROP DATABASE [IF EXISTS] database_name [CASCADE];
```

**Parameters:**

*   `IF EXISTS`: If specified, the database will only be dropped if a database with the same name already exists.
*   `database_name`: The name of the database to drop.
*   `CASCADE`: If specified, all objects within the database (tables, indexes, etc.) will be dropped as well.

### USE

Selects a database to use for subsequent queries.

**Syntax:**

```sql
USE database_name;
```

**Parameters:**

*   `database_name`: The name of the database to use.

### SHOW DATABASES

Lists the available databases.

**Syntax:**

```sql
SHOW DATABASES [LIKE 'pattern'];
```

**Parameters:**

*   `LIKE 'pattern'`: If specified, only databases with names matching the pattern will be listed.

### CREATE TABLE

Creates a new table.

**Syntax:**

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
    column_name data_type [column_constraint],
    ...
    [table_constraint]
);
```

**Parameters:**

*   `IF NOT EXISTS`: If specified, the table will only be created if a table with the same name does not already exist.
*   `table_name`: The name of the new table.
*   `column_name`: The name of a column.
*   `data_type`: The data type of the column.
*   `column_constraint`: A constraint that applies to the column.
*   `table_constraint`: A constraint that applies to the table.

**Data Types:**

*   `BOOLEAN`
*   `SMALLINT`
*   `INTEGER`
*   `BIGINT`
*   `REAL`
*   `DOUBLE`
*   `TEXT`
*   `VARCHAR(n)`
*   `CHAR(n)`
*   `BYTEA`
*   `JSON`
*   `JSONB`
*   `UUID`
*   `VECTOR(n)`
*   `AUDIO`
*   `VIDEO`
*   `IMAGE`
*   `PDF`
*   `TIMESTAMP`
*   `DATE`
*   `TIME`
*   `DECIMAL(p, s)`

**Column Constraints:**

*   `PRIMARY KEY`
*   `UNIQUE`
*   `NOT NULL`
*   `CHECK (expression)`
*   `DEFAULT expression`
*   `REFERENCES foreign_table (foreign_column)`

**Table Constraints:**

*   `PRIMARY KEY (column_name, ...)`
*   `UNIQUE (column_name, ...)`
*   `CHECK (expression)`
*   `FOREIGN KEY (column_name, ...) REFERENCES foreign_table (foreign_column, ...)`

### DROP TABLE

Drops an existing table.

**Syntax:**

```sql
DROP TABLE [IF EXISTS] table_name [CASCADE];
```

**Parameters:**

*   `IF EXISTS`: If specified, the table will only be dropped if a table with the same name already exists.
*   `table_name`: The name of the table to drop.
*   `CASCADE`: If specified, all objects that depend on the table (indexes, etc.) will be dropped as well.

### ALTER TABLE

Modifies an existing table.

**Syntax:**

```sql
ALTER TABLE table_name action;
```

**Actions:**

*   `ADD COLUMN column_name data_type [column_constraint]`
*   `DROP COLUMN column_name`
*   `RENAME COLUMN old_name TO new_name`
*   `ALTER COLUMN column_name TYPE new_data_type`
*   `ADD table_constraint`
*   `DROP CONSTRAINT constraint_name`

### CREATE INDEX

Creates a new index on a table.

**Syntax:**

```sql
CREATE [UNIQUE] INDEX [IF NOT EXISTS] index_name ON table_name (column_name [ASC | DESC], ...);
```

**Parameters:**

*   `UNIQUE`: If specified, the index will enforce that all values in the indexed column(s) are unique.
*   `IF NOT EXISTS`: If specified, the index will only be created if an index with the same name does not already exist.
*   `index_name`: The name of the new index.
*   `table_name`: The name of the table to create the index on.
*   `column_name`: The name of a column to include in the index.
*   `ASC | DESC`: The sort order for the column.

### DROP INDEX

Drops an existing index.

**Syntax:**

```sql
DROP INDEX [IF EXISTS] index_name;
```

**Parameters:**

*   `IF EXISTS`: If specified, the index will only be dropped if an index with the same name already exists.
*   `index_name`: The name of the index to drop.

## Data Manipulation Language (DML)

DML commands are used to manipulate data in the database.

### INSERT

Inserts new rows into a table.

**Syntax:**

```sql
INSERT INTO table_name [(column_name, ...)]
VALUES (value, ...), ...;
```

**Parameters:**

*   `table_name`: The name of the table to insert into.
*   `column_name`: The name of a column to insert into.
*   `value`: The value to insert.

### UPDATE

Updates existing rows in a table.

**Syntax:**

```sql
UPDATE table_name
SET column_name = value, ...
[WHERE condition];
```

**Parameters:**

*   `table_name`: The name of the table to update.
*   `column_name`: The name of a column to update.
*   `value`: The new value for the column.
*   `WHERE condition`: A condition that specifies which rows to update.

### DELETE

Deletes existing rows from a table.

**Syntax:**

```sql
DELETE FROM table_name
[WHERE condition];
```

**Parameters:**

*   `table_name`: The name of the table to delete from.
*   `WHERE condition`: A condition that specifies which rows to delete.

## Query Language

### SELECT

Retrieves data from the database.

**Syntax:**

```sql
SELECT [ALL | DISTINCT] column_name, ...
FROM table_name
[WHERE condition]
[GROUP BY column_name, ...]
[HAVING condition]
[ORDER BY column_name [ASC | DESC], ...]
[LIMIT count]
[OFFSET start];
```

**Parameters:**

*   `ALL`: Returns all rows.
*   `DISTINCT`: Returns only distinct rows.
*   `column_name`: The name of a column to retrieve.
*   `table_name`: The name of the table to retrieve from.
*   `WHERE condition`: A condition that filters the rows.
*   `GROUP BY column_name`: Groups the rows by the specified column(s).
*   `HAVING condition`: Filters the grouped rows.
*   `ORDER BY column_name [ASC | DESC]`: Sorts the rows by the specified column(s).
*   `LIMIT count`: Limits the number of rows returned.
*   `OFFSET start`: Skips the specified number of rows.

## Transaction Control Language (TCL)

TCL commands are used to manage transactions in the database.

### BEGIN TRANSACTION

Starts a new transaction.

**Syntax:**

```sql
BEGIN [TRANSACTION];
```

### COMMIT

Commits the current transaction.

**Syntax:**

```sql
COMMIT;
```

### ROLLBACK

Rolls back the current transaction.

**Syntax:**

```sql
ROLLBACK;
```
### Math Functions Added:

  - EXP - Exponential function
  - LOG/LN - Natural logarithm
  - LOG10 - Base-10 logarithm
  - SIGN - Returns -1, 0, or 1 based on sign
  - TRUNCATE/TRUNC - Truncate to specified decimal places
  - PI - Mathematical constant π
  - RAND/RANDOM - Random number generator
  - Trigonometric: SIN, COS, TAN, ASIN, ACOS, ATAN
  - DEGREES/RADIANS - Angle conversion

### String Functions Added:

  - LEFT/RIGHT - Extract characters from start/end
  - LPAD/RPAD - Pad strings to specified length
  - REPEAT - Repeat string n times
  - REVERSE - Reverse string characters
  - INSTR/POSITION - Find substring position
  - ASCII/CHAR/CHR - ASCII code conversions
  - INITCAP - Capitalize first letter of each word
  - Hash functions: MD5, SHA1, SHA256

### Date/Time Functions Added:

  - NOW/CURRENT_TIMESTAMP - Current date and time
  - CURRENT_DATE - Current date only
  - CURRENT_TIME - Current time only
  - YEAR/MONTH/DAY - Extract date components
  - HOUR/MINUTE/SECOND - Extract time components
  - UNIX_TIMESTAMP - Convert to/from Unix timestamp

### Other Functions Added:

  - GREATEST - Return maximum from list of values
  - LEAST - Return minimum from list of values
  - IF/IIF - Simple conditional (if-then-else)
  - IFNULL/ISNULL - Return alternative if null

### Date Formatting Functions:

  - DATE_FORMAT(date, format) - Format date/time with custom format strings
    - Supports MySQL-style format codes: %Y, %m, %d, %H, %i, %s, etc.
    - Alternative formats: YYYY, MM, DD, HH, mm, ss
    - Examples: '%Y-%m-%d', '%m/%d/%Y', '%W, %M %d, %Y'
  - STR_TO_DATE(string, format) - Parse string into date using format

### Date Arithmetic Functions:

  - DATE_ADD(date, interval, type) - Add interval to date
    - Types: SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, YEAR
  - DATE_SUB(date, interval, type) - Subtract interval from date
  - DATEDIFF(date1, date2) - Days between two dates

### Date Information Functions:

  - LAST_DAY(date) - Last day of the month
  - DAYNAME(date) - Weekday name (Monday, Tuesday, etc.)
  - MONTHNAME(date) - Month name (January, February, etc.)
  - QUARTER(date) - Quarter (1-4)
  - WEEK/WEEKOFYEAR(date) - Week number of year
  - DAYOFWEEK(date) - Day of week (1=Sunday, 7=Saturday)
  - DAYOFYEAR(date) - Day number of year (1-366)

  Common Usage Examples:

  -- Format current date/time
  DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%s')  -- '2024-12-25 14:30:45'
  DATE_FORMAT(NOW(), '%m/%d/%Y')           -- '12/25/2024' (US format)
  DATE_FORMAT(NOW(), '%d/%m/%Y')           -- '25/12/2024' (EU format)

  -- Date arithmetic
  DATE_ADD('2024-01-15', 30, 'DAY')        -- Add 30 days
  DATE_SUB(NOW(), 1, 'MONTH')              -- One month ago
  DATEDIFF('2024-12-31', NOW())            -- Days until year end

  -- Date information
  DAYNAME('2024-12-25')                    -- 'Wednesday'
  QUARTER('2024-07-15')                    -- 3
  WEEK('2024-12-25')                       -- 52

## AI Functions

AIDB provides a number of built-in functions for performing AI and vector operations.

### embed

Computes an embedding for the given text.

**Syntax:**

```sql
embed(text)
```

**Parameters:**

*   `text`: The text to compute the embedding for.

### similarity

Computes the similarity between two embeddings.

**Syntax:**

```sql
similarity(embedding1, embedding2)
```

**Parameters:**

*   `embedding1`: The first embedding.
*   `embedding2`: The second embedding.

### cosine_similarity

Computes the cosine similarity between two embeddings.

**Syntax:**

```sql
cosine_similarity(embedding1, embedding2)
```

**Parameters:**

*   `embedding1`: The first embedding.
*   `embedding2`: The second embedding.

### euclidean_distance

Computes the Euclidean distance between two embeddings.

**Syntax:**

```sql
euclidean_distance(embedding1, embedding2)
```

**Parameters:**

*   `embedding1`: The first embedding.
*   `embedding2`: The second embedding.

### vector_search

Performs a vector search on a collection of embeddings.

**Syntax:**

```sql
vector_search(embedding, query_embedding, k)
```

**Parameters:**

*   `embedding`: The embedding to search.
*   `query_embedding`: The query embedding.
*   `k`: The number of nearest neighbors to return.

### semantic_search

Performs a semantic search on a collection of embeddings.

**Syntax:**

```sql
semantic_search(embedding, query_embedding, k)
```

**Parameters:**

*   `embedding`: The embedding to search.
*   `query_embedding`: The query embedding.
*   `k`: The number of nearest neighbors to return.

### classify

Classifies the given text into one of the specified categories.

**Syntax:**

```sql
classify(text, categories)
```

**Parameters:**

*   `text`: The text to classify.
*   `categories`: A list of categories to classify the text into.

### predict

Makes a prediction based on the given input.

**Syntax:**

```sql
predict(input)
```

**Parameters:**

*   `input`: The input to the model.

### generate

Generates text based on the given prompt.

**Syntax:**

```sql
generate(prompt)
```

**Parameters:**

*   `prompt`: The prompt to generate text from.

### extract_entities

Extracts entities from the given text.

**Syntax:**

```sql
extract_entities(text)
```

**Parameters:**

*   `text`: The text to extract entities from.

### sentiment

Computes the sentiment of the given text.

**Syntax:**

```sql
sentiment(text)
```

**Parameters:**

*   `text`: The text to compute the sentiment of.

### summarize

Summarizes the given text.

**Syntax:**

```sql
summarize(text)
```

**Parameters:**

*   `text`: The text to summarize.

## AutoML Commands

AIDB provides a set of commands for managing AutoML experiments and models.

### CREATE EXPERIMENT

Creates a new AutoML experiment.

**Syntax:**

```sql
CREATE EXPERIMENT experiment_name
FROM (SELECT ...)
TARGET target_column
[OPTIONS (option_name = 'option_value', ...)];
```

**Parameters:**

*   `experiment_name`: The name of the new experiment.
*   `SELECT ...`: A query that provides the training data.
*   `target_column`: The name of the column to predict.
*   `OPTIONS`: A list of options for the experiment.

  algorithms = ['logistic_regression', 'random_forest', 'gradient_boosting']

  All Classification Algorithms

  algorithms = ['logistic_regression', 'random_forest', 'gradient_boosting',
                'neural_network', 'knn', 'svm', 'naive_bayes']

  Fast Algorithms Only

  algorithms = ['logistic_regression', 'naive_bayes', 'knn']

  Deep Learning Only

  algorithms = ['neural_network']

  Algorithm Details

  | Algorithm           | Best For                             | Speed     | Accuracy        |
  |---------------------|--------------------------------------|-----------|-----------------|
  | logistic_regression | Binary classification, interpretable | Fast      | Good            |
  | linear_regression   | Simple regression, interpretable     | Fast      | Good for linear |
  | random_forest       | General purpose, robust              | Medium    | High            |
  | gradient_boosting   | High accuracy, competitions          | Slow      | Very High       |
  | neural_network      | Complex patterns, large data         | Slow*     | High            |
  | knn                 | Simple, local patterns               | Fast      | Medium          |
  | svm                 | Binary classification, kernels       | Medium    | High            |
  | naive_bayes         | Text classification, simple          | Very Fast | Medium          |

### SHOW EXPERIMENTS

Lists the available AutoML experiments.

**Syntax:**

```sql
SHOW EXPERIMENTS;
```

### DESCRIBE EXPERIMENT

Describes an AutoML experiment.

**Syntax:**

```sql
DESCRIBE EXPERIMENT experiment_name;
```

**Parameters:**

*   `experiment_name`: The name of the experiment to describe.

### START EXPERIMENT

Starts an AutoML experiment.

**Syntax:**

```sql
START EXPERIMENT experiment_name;
```

**Parameters:**

*   `experiment_name`: The name of the experiment to start.

### STOP EXPERIMENT

Stops an AutoML experiment.

**Syntax:**

```sql
STOP EXPERIMENT experiment_name;
```

**Parameters:**

*   `experiment_name`: The name of the experiment to stop.

### DROP EXPERIMENT

Drops an AutoML experiment.

**Syntax:**

```sql
DROP EXPERIMENT experiment_name;
```

**Parameters:**

*   `experiment_name`: The name of the experiment to drop.

### GET MODELS

Gets the models from an AutoML experiment.

**Syntax:**

```sql
GET MODELS FROM experiment_name;
```

**Parameters:**

*   `experiment_name`: The name of the experiment to get the models from.

### DEPLOY MODEL

Deploys a model from an AutoML experiment.

**Syntax:**

```sql
DEPLOY MODEL model_name
FROM experiment_name;
```

**Parameters:**

*   `model_name`: The name of the model to deploy.
*   `experiment_name`: The name of the experiment to deploy the model from.

### SHOW MODELS

Lists the deployed models.

**Syntax:**

```sql
SHOW MODELS;
```

### DESCRIBE MODEL

Describes a deployed model.

**Syntax:**

```sql
DESCRIBE MODEL model_name;
```

**Parameters:**

*   `model_name`: The name of the model to describe.

### DROP MODEL

Drops a deployed model.

**Syntax:**

```sql
DROP MODEL model_name;
```

**Parameters:**

*   `model_name`: The name of the model to drop.

### PREDICT ... USING ...

Makes predictions using a deployed model.

**Syntax:**

```sql
PREDICT prediction_column, ...
USING model_name
FROM (SELECT ...);
```

**Parameters:**

*   `prediction_column`: The name of the column to store the prediction in.
*   `model_name`: The name of the model to use for prediction.
*   `SELECT ...`: A query that provides the data to predict on.

## Triggers and Procedures

AIDB supports triggers and stored procedures to automate and extend the functionality of the database.

### CREATE TRIGGER

Creates a new trigger.

**Syntax:**

```sql
CREATE [OR REPLACE] TRIGGER trigger_name
{BEFORE | AFTER} {INSERT | UPDATE | DELETE} ON table_name
[FOR EACH ROW]
[WHEN condition]
EXECUTE PROCEDURE procedure_name (arguments);
```

**Parameters:**

*   `OR REPLACE`: If specified, the trigger will be replaced if it already exists.
*   `trigger_name`: The name of the new trigger.
*   `BEFORE | AFTER`: The timing of the trigger.
*   `INSERT | UPDATE | DELETE`: The event that activates the trigger.
*   `table_name`: The name of the table the trigger is on.
*   `FOR EACH ROW`: The trigger will be executed for each row affected by the event.
*   `WHEN condition`: A condition that must be true for the trigger to be executed.
*   `procedure_name`: The name of the procedure to execute.
*   `arguments`: The arguments to pass to the procedure.

### DROP TRIGGER

Drops an existing trigger.

**Syntax:**

```sql
DROP TRIGGER [IF EXISTS] trigger_name ON table_name;
```

**Parameters:**

*   `IF EXISTS`: If specified, the trigger will only be dropped if it already exists.
*   `trigger_name`: The name of the trigger to drop.
*   `table_name`: The name of the table the trigger is on.

### CREATE PROCEDURE

Creates a new stored procedure.

**Syntax:**

```sql
CREATE [OR REPLACE] PROCEDURE procedure_name (arguments)
AS $
BEGIN
    -- procedure body
END;
$ LANGUAGE plpgsql;
```

**Parameters:**

*   `OR REPLACE`: If specified, the procedure will be replaced if it already exists.
*   `procedure_name`: The name of the new procedure.
*   `arguments`: The arguments to the procedure.

### DROP PROCEDURE

Drops an existing stored procedure.

**Syntax:**

```sql
DROP PROCEDURE [IF EXISTS] procedure_name;
```

**Parameters:**

*   `IF EXISTS`: If specified, the procedure will only be dropped if it already exists.
*   `procedure_name`: The name of the procedure to drop.

### CALL

Calls a stored procedure.

**Syntax:**

```sql
CALL procedure_name (arguments);
```

**Parameters:**

*   `procedure_name`: The name of the procedure to call.
*   `arguments`: The arguments to pass to the procedure.

## Natural Language Queries

AIDB can understand and execute natural language queries.

### ASK

Executes a natural language query.

**Syntax:**

```sql
ASK '<natural_language_query>';
```

**Parameters:**

*   `natural_language_query`: The natural language query to execute.

### EXPLAIN NATURAL

Explains how a natural language query will be executed.

**Syntax:**

```sql
EXPLAIN NATURAL '<natural_language_query>';
```

**Parameters:**

*   `natural_language_query`: The natural language query to explain.
