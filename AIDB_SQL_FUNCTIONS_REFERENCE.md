# AIDB SQL Functions Reference

This document provides a comprehensive reference for all SQL functions implemented in AIDB, including standard SQL functions, statistical functions, window functions, AI/ML functions, and multimedia functions.

## Table of Contents

1. [Aggregate Functions](#aggregate-functions)
2. [Window Functions](#window-functions)
3. [Statistical Functions](#statistical-functions)
4. [String Functions](#string-functions)
5. [Date and Time Functions](#date-and-time-functions)
6. [Mathematical Functions](#mathematical-functions)
7. [AI and ML Functions](#ai-and-ml-functions)
8. [Vector Functions](#vector-functions)
9. [Multimedia Functions](#multimedia-functions)
10. [Utility Functions](#utility-functions)

---

## Aggregate Functions

Aggregate functions operate on groups of rows and return a single value for each group.

### COUNT
**Syntax**: `COUNT(column)` or `COUNT(*)`
**Description**: Returns the number of rows
**Parameters**:
- `column`: Column to count (NULL values are excluded)
- `*`: Count all rows including NULL values
**Return Type**: Integer
**Example**:
```sql
SELECT COUNT(*) FROM users;
SELECT COUNT(email) FROM users; -- Excludes NULL emails
```

### SUM
**Syntax**: `SUM(column)`
**Description**: Returns the sum of numeric values
**Parameters**:
- `column`: Numeric column to sum
**Return Type**: Float64
**Example**:
```sql
SELECT SUM(amount) FROM orders;
SELECT SUM(price * quantity) FROM order_items;
```

### AVG
**Syntax**: `AVG(column)`
**Description**: Returns the average of numeric values
**Parameters**:
- `column`: Numeric column to average
**Return Type**: Float64
**Example**:
```sql
SELECT AVG(salary) FROM employees;
SELECT department, AVG(salary) FROM employees GROUP BY department;
```

### MIN
**Syntax**: `MIN(column)`
**Description**: Returns the minimum value
**Parameters**:
- `column`: Column to find minimum value
**Return Type**: Same as input column type
**Example**:
```sql
SELECT MIN(price) FROM products;
SELECT MIN(created_at) FROM orders;
```

### MAX
**Syntax**: `MAX(column)`
**Description**: Returns the maximum value
**Parameters**:
- `column`: Column to find maximum value
**Return Type**: Same as input column type
**Example**:
```sql
SELECT MAX(price) FROM products;
SELECT MAX(updated_at) FROM users;
```

### VECTOR_CENTROID
**Syntax**: `VECTOR_CENTROID(vector_column)`
**Description**: Calculates the centroid (average) of a set of vectors
**Parameters**:
- `vector_column`: Column containing vector data
**Return Type**: Vector
**Example**:
```sql
SELECT VECTOR_CENTROID(embedding) FROM document_embeddings WHERE category = 'tech';
```

---

## Window Functions

Window functions perform calculations across a set of rows related to the current row.

### ROW_NUMBER
**Syntax**: `ROW_NUMBER() OVER ([PARTITION BY column] [ORDER BY column])`
**Description**: Assigns a unique sequential integer to rows within a partition
**Parameters**: None
**Return Type**: Integer
**Example**:
```sql
SELECT name, salary, ROW_NUMBER() OVER (ORDER BY salary DESC) as rank
FROM employees;

SELECT name, salary, ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as dept_rank
FROM employees;
```

### RANK
**Syntax**: `RANK() OVER (ORDER BY column)`
**Description**: Assigns a rank to each row, with gaps in rank for tied values
**Parameters**: None (requires ORDER BY)
**Return Type**: Integer
**Example**:
```sql
SELECT name, score, RANK() OVER (ORDER BY score DESC) as rank
FROM students;
```

### DENSE_RANK
**Syntax**: `DENSE_RANK() OVER (ORDER BY column)`
**Description**: Assigns a rank to each row, without gaps in rank for tied values
**Parameters**: None (requires ORDER BY)
**Return Type**: Integer
**Example**:
```sql
SELECT name, score, DENSE_RANK() OVER (ORDER BY score DESC) as dense_rank
FROM students;
```

### LAG
**Syntax**: `LAG(column [, offset [, default]]) OVER ([PARTITION BY column] ORDER BY column)`
**Description**: Returns the value from a previous row
**Parameters**:
- `column`: Column to retrieve value from
- `offset`: Number of rows back (default: 1)
- `default`: Default value when no previous row exists
**Return Type**: Same as input column type
**Example**:
```sql
SELECT date, price, LAG(price, 1, 0) OVER (ORDER BY date) as prev_price
FROM stock_prices;

SELECT date, sales, LAG(sales, 1) OVER (PARTITION BY region ORDER BY date) as prev_sales
FROM monthly_sales;
```

### LEAD
**Syntax**: `LEAD(column [, offset [, default]]) OVER ([PARTITION BY column] ORDER BY column)`
**Description**: Returns the value from a following row
**Parameters**:
- `column`: Column to retrieve value from
- `offset`: Number of rows forward (default: 1)
- `default`: Default value when no following row exists
**Return Type**: Same as input column type
**Example**:
```sql
SELECT date, price, LEAD(price, 1, 0) OVER (ORDER BY date) as next_price
FROM stock_prices;
```

### SUM (Window)
**Syntax**: `SUM(column) OVER ([PARTITION BY column] [ORDER BY column] [ROWS/RANGE frame])`
**Description**: Running sum over a window frame
**Parameters**:
- `column`: Numeric column to sum
**Return Type**: Float64
**Example**:
```sql
SELECT date, amount, SUM(amount) OVER (ORDER BY date ROWS UNBOUNDED PRECEDING) as running_total
FROM transactions;

SELECT date, amount, SUM(amount) OVER (ORDER BY date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) as rolling_3day_sum
FROM daily_sales;
```

### AVG (Window)
**Syntax**: `AVG(column) OVER ([PARTITION BY column] [ORDER BY column] [ROWS/RANGE frame])`
**Description**: Moving average over a window frame
**Parameters**:
- `column`: Numeric column to average
**Return Type**: Float64
**Example**:
```sql
SELECT date, price, AVG(price) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) as moving_avg_7day
FROM stock_prices;
```

### STDDEV (Window)
**Syntax**: `STDDEV(column) OVER ([PARTITION BY column] [ORDER BY column] [ROWS/RANGE frame])`
**Description**: Standard deviation over a window frame
**Parameters**:
- `column`: Numeric column
**Return Type**: Float64
**Example**:
```sql
SELECT date, price, STDDEV(price) OVER (ORDER BY date ROWS BETWEEN 29 PRECEDING AND CURRENT ROW) as volatility_30day
FROM stock_prices;
```

---

## Statistical Functions

Advanced statistical functions for data analysis.

### STDDEV / STDDEV_SAMP
**Syntax**: `STDDEV(column)` or `STDDEV_SAMP(column)`
**Description**: Sample standard deviation (n-1 denominator)
**Parameters**:
- `column`: Numeric column
**Return Type**: Float64
**Example**:
```sql
SELECT STDDEV(salary) FROM employees;
SELECT department, STDDEV(salary) FROM employees GROUP BY department;
```

### STDDEV_POP
**Syntax**: `STDDEV_POP(column)`
**Description**: Population standard deviation (n denominator)
**Parameters**:
- `column`: Numeric column
**Return Type**: Float64
**Example**:
```sql
SELECT STDDEV_POP(test_score) FROM students;
```

### VARIANCE / VAR_SAMP
**Syntax**: `VARIANCE(column)` or `VAR_SAMP(column)`
**Description**: Sample variance (n-1 denominator)
**Parameters**:
- `column`: Numeric column
**Return Type**: Float64
**Example**:
```sql
SELECT VARIANCE(response_time) FROM api_calls;
```

### VAR_POP
**Syntax**: `VAR_POP(column)`
**Description**: Population variance (n denominator)
**Parameters**:
- `column`: Numeric column
**Return Type**: Float64
**Example**:
```sql
SELECT VAR_POP(measurement) FROM sensor_data;
```

### MEDIAN
**Syntax**: `MEDIAN(column)`
**Description**: 50th percentile value
**Parameters**:
- `column`: Numeric column
**Return Type**: Float64
**Example**:
```sql
SELECT MEDIAN(income) FROM households;
SELECT city, MEDIAN(house_price) FROM real_estate GROUP BY city;
```

### MODE
**Syntax**: `MODE(column)`
**Description**: Most frequently occurring value
**Parameters**:
- `column`: Any column type
**Return Type**: String (formatted representation)
**Example**:
```sql
SELECT MODE(status) FROM orders;
SELECT MODE(favorite_color) FROM user_preferences;
```

### PERCENTILE_CONT
**Syntax**: `PERCENTILE_CONT(percentile, column)`
**Description**: Continuous percentile with linear interpolation
**Parameters**:
- `percentile`: Value between 0.0 and 1.0
- `column`: Numeric column
**Return Type**: Float64
**Example**:
```sql
SELECT PERCENTILE_CONT(0.95, response_time) FROM api_calls; -- 95th percentile
SELECT PERCENTILE_CONT(0.25, salary) FROM employees; -- First quartile
```

### PERCENTILE_DISC
**Syntax**: `PERCENTILE_DISC(percentile, column)`
**Description**: Discrete percentile (returns actual value from dataset)
**Parameters**:
- `percentile`: Value between 0.0 and 1.0
- `column`: Any column type
**Return Type**: Same as input column type
**Example**:
```sql
SELECT PERCENTILE_DISC(0.50, age) FROM users; -- Median age (actual value)
```

### CORR
**Syntax**: `CORR(x_column, y_column)`
**Description**: Pearson correlation coefficient between two variables
**Parameters**:
- `x_column`: First numeric column
- `y_column`: Second numeric column
**Return Type**: Float64 (-1.0 to 1.0)
**Example**:
```sql
SELECT CORR(advertising_spend, sales) FROM monthly_metrics;
SELECT CORR(temperature, ice_cream_sales) FROM daily_sales;
```

### REGR_SLOPE
**Syntax**: `REGR_SLOPE(y_column, x_column)`
**Description**: Slope of linear regression line
**Parameters**:
- `y_column`: Dependent variable
- `x_column`: Independent variable
**Return Type**: Float64
**Example**:
```sql
SELECT REGR_SLOPE(sales, advertising_spend) FROM monthly_data;
```

### REGR_INTERCEPT
**Syntax**: `REGR_INTERCEPT(y_column, x_column)`
**Description**: Y-intercept of linear regression line
**Parameters**:
- `y_column`: Dependent variable
- `x_column`: Independent variable
**Return Type**: Float64
**Example**:
```sql
SELECT REGR_INTERCEPT(sales, advertising_spend) FROM monthly_data;
```

---

## String Functions

Functions for manipulating and analyzing text data.

### UPPER
**Syntax**: `UPPER(string)`
**Description**: Converts string to uppercase
**Parameters**:
- `string`: Input string
**Return Type**: String
**Example**:
```sql
SELECT UPPER(name) FROM users;
SELECT UPPER('hello world'); -- Returns 'HELLO WORLD'
```

### LOWER
**Syntax**: `LOWER(string)`
**Description**: Converts string to lowercase
**Parameters**:
- `string`: Input string
**Return Type**: String
**Example**:
```sql
SELECT LOWER(email) FROM users;
SELECT LOWER('HELLO WORLD'); -- Returns 'hello world'
```

### LENGTH / LEN
**Syntax**: `LENGTH(string)` or `LEN(string)`
**Description**: Returns the length of a string, bytes, or vector
**Parameters**:
- `string`: Input string, bytes, or vector
**Return Type**: Integer
**Example**:
```sql
SELECT LENGTH(description) FROM products;
SELECT name FROM users WHERE LENGTH(name) > 10;
```

### SUBSTRING / SUBSTR
**Syntax**: `SUBSTRING(string, start [, length])` or `SUBSTR(string, start [, length])`
**Description**: Extracts a substring
**Parameters**:
- `string`: Input string
- `start`: Starting position (1-based)
- `length`: Number of characters (optional)
**Return Type**: String
**Example**:
```sql
SELECT SUBSTRING(name, 1, 3) FROM users; -- First 3 characters
SELECT SUBSTRING(phone_number, 1, 3) as area_code FROM contacts;
SELECT SUBSTR(description, 10) FROM products; -- From position 10 to end
```

### CONCAT
**Syntax**: `CONCAT(string1, string2, ...)`
**Description**: Concatenates multiple strings
**Parameters**:
- `string1, string2, ...`: Strings to concatenate
**Return Type**: String
**Example**:
```sql
SELECT CONCAT(first_name, ' ', last_name) as full_name FROM users;
SELECT CONCAT('Hello ', name, '!') as greeting FROM users;
```

### TRIM
**Syntax**: `TRIM(string)`
**Description**: Removes leading and trailing whitespace
**Parameters**:
- `string`: Input string
**Return Type**: String
**Example**:
```sql
SELECT TRIM(name) FROM users;
UPDATE users SET email = TRIM(email);
```

### LTRIM
**Syntax**: `LTRIM(string)`
**Description**: Removes leading whitespace
**Parameters**:
- `string`: Input string
**Return Type**: String
**Example**:
```sql
SELECT LTRIM(name) FROM users;
```

### RTRIM
**Syntax**: `RTRIM(string)`
**Description**: Removes trailing whitespace
**Parameters**:
- `string`: Input string
**Return Type**: String
**Example**:
```sql
SELECT RTRIM(name) FROM users;
```

---

## Date and Time Functions

Functions for working with dates, times, and intervals.

### YEAR
**Syntax**: `YEAR(date)`
**Description**: Extracts the year from a date
**Parameters**:
- `date`: Date/datetime string
**Return Type**: Integer
**Example**:
```sql
SELECT YEAR(created_at) FROM orders;
SELECT YEAR('2023-12-25'); -- Returns 2023
```

### MONTH
**Syntax**: `MONTH(date)`
**Description**: Extracts the month from a date
**Parameters**:
- `date`: Date/datetime string
**Return Type**: Integer (1-12)
**Example**:
```sql
SELECT MONTH(created_at) FROM orders;
SELECT MONTH('2023-12-25'); -- Returns 12
```

### DAY
**Syntax**: `DAY(date)`
**Description**: Extracts the day from a date
**Parameters**:
- `date`: Date/datetime string
**Return Type**: Integer (1-31)
**Example**:
```sql
SELECT DAY(created_at) FROM orders;
SELECT DAY('2023-12-25'); -- Returns 25
```

### HOUR
**Syntax**: `HOUR(datetime)`
**Description**: Extracts the hour from a datetime
**Parameters**:
- `datetime`: Datetime string
**Return Type**: Integer (0-23)
**Example**:
```sql
SELECT HOUR(created_at) FROM orders;
SELECT HOUR('2023-12-25 14:30:00'); -- Returns 14
```

### MINUTE
**Syntax**: `MINUTE(datetime)`
**Description**: Extracts the minute from a datetime
**Parameters**:
- `datetime`: Datetime string
**Return Type**: Integer (0-59)
**Example**:
```sql
SELECT MINUTE(created_at) FROM orders;
SELECT MINUTE('2023-12-25 14:30:00'); -- Returns 30
```

### DAYNAME
**Syntax**: `DAYNAME(date)`
**Description**: Returns the day name (Monday, Tuesday, etc.)
**Parameters**:
- `date`: Date/datetime string
**Return Type**: String
**Example**:
```sql
SELECT DAYNAME(created_at) FROM orders;
SELECT DAYNAME('2023-12-25'); -- Returns 'Monday'
```

### MONTHNAME
**Syntax**: `MONTHNAME(date)`
**Description**: Returns the month name (January, February, etc.)
**Parameters**:
- `date`: Date/datetime string
**Return Type**: String
**Example**:
```sql
SELECT MONTHNAME(created_at) FROM orders;
SELECT MONTHNAME('2023-12-25'); -- Returns 'December'
```

### DAYOFWEEK
**Syntax**: `DAYOFWEEK(date)`
**Description**: Returns the day of week (1=Sunday, 2=Monday, ..., 7=Saturday)
**Parameters**:
- `date`: Date/datetime string
**Return Type**: Integer (1-7)
**Example**:
```sql
SELECT DAYOFWEEK(created_at) FROM orders;
SELECT DAYOFWEEK('2023-12-25'); -- Returns 2 (Monday)
```

### DAYOFYEAR
**Syntax**: `DAYOFYEAR(date)`
**Description**: Returns the day of year (1-366)
**Parameters**:
- `date`: Date/datetime string
**Return Type**: Integer (1-366)
**Example**:
```sql
SELECT DAYOFYEAR(created_at) FROM orders;
SELECT DAYOFYEAR('2023-12-25'); -- Returns 359
```

### LAST_DAY
**Syntax**: `LAST_DAY(date)`
**Description**: Returns the last day of the month for the given date
**Parameters**:
- `date`: Date/datetime string
**Return Type**: String (date format)
**Example**:
```sql
SELECT LAST_DAY('2023-02-15'); -- Returns '2023-02-28'
SELECT LAST_DAY('2024-02-15'); -- Returns '2024-02-29' (leap year)
```

### DATE_ADD
**Syntax**: `DATE_ADD(date, interval, type)`
**Description**: Adds an interval to a date
**Parameters**:
- `date`: Date/datetime string
- `interval`: Number to add
- `type`: Interval type (SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, YEAR)
**Return Type**: String (datetime format)
**Example**:
```sql
SELECT DATE_ADD('2023-12-25', 7, 'DAY'); -- Returns '2024-01-01'
SELECT DATE_ADD('2023-12-25 10:00:00', 2, 'HOUR'); -- Returns '2023-12-25 12:00:00'
```

---

## Mathematical Functions

Functions for mathematical calculations.

### ABS
**Syntax**: `ABS(number)`
**Description**: Returns the absolute value
**Parameters**:
- `number`: Numeric value
**Return Type**: Same as input type
**Example**:
```sql
SELECT ABS(-42); -- Returns 42
SELECT ABS(price - average_price) FROM products;
```

### ROUND
**Syntax**: `ROUND(number [, precision])`
**Description**: Rounds to specified decimal places
**Parameters**:
- `number`: Numeric value
- `precision`: Number of decimal places (default: 0)
**Return Type**: Float64
**Example**:
```sql
SELECT ROUND(3.14159, 2); -- Returns 3.14
SELECT ROUND(amount) FROM transactions; -- Rounds to nearest integer
```

### CEIL / CEILING
**Syntax**: `CEIL(number)` or `CEILING(number)`
**Description**: Returns the smallest integer greater than or equal to the number
**Parameters**:
- `number`: Numeric value
**Return Type**: Float64
**Example**:
```sql
SELECT CEIL(3.14); -- Returns 4.0
SELECT CEILING(-2.8); -- Returns -2.0
```

### FLOOR
**Syntax**: `FLOOR(number)`
**Description**: Returns the largest integer less than or equal to the number
**Parameters**:
- `number`: Numeric value
**Return Type**: Float64
**Example**:
```sql
SELECT FLOOR(3.14); -- Returns 3.0
SELECT FLOOR(-2.8); -- Returns -3.0
```

### SQRT
**Syntax**: `SQRT(number)`
**Description**: Returns the square root
**Parameters**:
- `number`: Non-negative numeric value
**Return Type**: Float64
**Example**:
```sql
SELECT SQRT(16); -- Returns 4.0
SELECT SQRT(area) FROM circles;
```

### POWER / POW
**Syntax**: `POWER(base, exponent)` or `POW(base, exponent)`
**Description**: Returns base raised to the power of exponent
**Parameters**:
- `base`: Numeric base value
- `exponent`: Numeric exponent value
**Return Type**: Float64
**Example**:
```sql
SELECT POWER(2, 3); -- Returns 8.0
SELECT POW(radius, 2) * 3.14159 as area FROM circles;
```

### MOD
**Syntax**: `MOD(dividend, divisor)`
**Description**: Returns the remainder of division
**Parameters**:
- `dividend`: Numeric dividend
- `divisor`: Numeric divisor
**Return Type**: Same as input type
**Example**:
```sql
SELECT MOD(10, 3); -- Returns 1
SELECT id FROM users WHERE MOD(id, 2) = 0; -- Even IDs
```

---

## AI and ML Functions

AIDB's built-in artificial intelligence and machine learning functions.

### EMBED
**Syntax**: `EMBED(text)`
**Description**: Generates vector embeddings for text
**Parameters**:
- `text`: Input text string
**Return Type**: Vector (float array)
**Example**:
```sql
SELECT EMBED(description) as embedding FROM products;
INSERT INTO documents (content, embedding) VALUES ('AI is transformative', EMBED('AI is transformative'));
```

### SEMANTIC_MATCH
**Syntax**: `SEMANTIC_MATCH(query, text [, threshold])`
**Description**: Checks if text semantically matches a query
**Parameters**:
- `query`: Query text
- `text`: Text to match against
- `threshold`: Similarity threshold (default: 0.7)
**Return Type**: Boolean
**Example**:
```sql
SELECT * FROM articles WHERE SEMANTIC_MATCH('artificial intelligence', content, 0.8);
SELECT * FROM products WHERE SEMANTIC_MATCH('laptop computer', description);
```

### SUMMARIZE
**Syntax**: `SUMMARIZE(text [, max_length])`
**Description**: Generates a summary of text
**Parameters**:
- `text`: Input text to summarize
- `max_length`: Maximum length of summary (optional)
**Return Type**: String
**Example**:
```sql
SELECT SUMMARIZE(article_content, 200) as summary FROM articles;
SELECT title, SUMMARIZE(description) as short_desc FROM products;
```

### EXTRACT_ENTITIES
**Syntax**: `EXTRACT_ENTITIES(text [, entity_types])`
**Description**: Extracts named entities from text
**Parameters**:
- `text`: Input text
- `entity_types`: JSON object specifying entity types (optional)
**Return Type**: JSON object with entities
**Example**:
```sql
SELECT EXTRACT_ENTITIES(content) as entities FROM news_articles;
SELECT EXTRACT_ENTITIES(review, '{"types": ["PERSON", "ORGANIZATION"]}') FROM reviews;
```

### TRANSLATE
**Syntax**: `TRANSLATE(text, target_language)`
**Description**: Translates text to target language
**Parameters**:
- `text`: Text to translate
- `target_language`: Target language code (e.g., 'es', 'fr', 'de')
**Return Type**: String
**Example**:
```sql
SELECT TRANSLATE(description, 'es') as spanish_desc FROM products;
SELECT TRANSLATE('Hello World', 'fr'); -- Returns 'Bonjour le monde'
```

### SENTIMENT_ANALYSIS
**Syntax**: `SENTIMENT_ANALYSIS(text)`
**Description**: Analyzes sentiment of text
**Parameters**:
- `text`: Input text
**Return Type**: JSON object with sentiment and confidence
**Example**:
```sql
SELECT SENTIMENT_ANALYSIS(review_text) as sentiment FROM reviews;
SELECT * FROM comments WHERE JSON_EXTRACT(SENTIMENT_ANALYSIS(content), '$.sentiment') = 'positive';
```

### GENERATE
**Syntax**: `GENERATE(prompt [, options])`
**Description**: Generates text based on a prompt
**Parameters**:
- `prompt`: Input prompt
- `options`: JSON object with generation options (optional)
**Return Type**: String
**Example**:
```sql
SELECT GENERATE('Write a product description for: ' || name) as ai_description FROM products;
SELECT GENERATE('Summarize this in one sentence: ' || content, '{"max_tokens": 50}') FROM articles;
```

---

## Vector Functions

Functions for working with vector embeddings and similarity.

### Vector Similarity Operators
**Syntax**:
- `vector1 <=> vector2` (Cosine similarity)
- `vector1 <-> vector2` (Euclidean distance)
- `vector1 <#> vector2` (Dot product)

**Description**: Calculate similarity/distance between vectors
**Parameters**:
- `vector1`, `vector2`: Vector values
**Return Type**: Float64
**Example**:
```sql
SELECT * FROM documents ORDER BY embedding <=> EMBED('AI technology') LIMIT 10;
SELECT doc1.title, doc2.title, doc1.embedding <-> doc2.embedding as distance
FROM documents doc1, documents doc2 WHERE doc1.id < doc2.id;
```

### Vector Similarity Functions
**Syntax**:
- `COSINE_SIMILARITY(vector1, vector2)`
- `EUCLIDEAN_DISTANCE(vector1, vector2)`
- `DOT_PRODUCT(vector1, vector2)`
- `MANHATTAN_DISTANCE(vector1, vector2)`

**Description**: Calculate various similarity/distance metrics
**Parameters**:
- `vector1`, `vector2`: Vector values
**Return Type**: Float64
**Example**:
```sql
SELECT COSINE_SIMILARITY(embedding1, embedding2) as similarity FROM vector_pairs;
SELECT * FROM documents WHERE EUCLIDEAN_DISTANCE(embedding, query_vector) < 0.5;
```

---

## Multimedia Functions

Functions for processing audio, video, images, and documents.

### EXTRACT_TEXT
**Syntax**: `EXTRACT_TEXT(multimedia_data)`
**Description**: Extracts text content from multimedia files
**Parameters**:
- `multimedia_data`: Audio, video, image, or PDF data
**Return Type**: String
**Example**:
```sql
SELECT EXTRACT_TEXT(pdf_data) as content FROM documents;
SELECT EXTRACT_TEXT(image_data) as ocr_text FROM scanned_docs;
```

### TRANSCRIBE
**Syntax**: `TRANSCRIBE(audio_or_video)`
**Description**: Transcribes speech from audio or video
**Parameters**:
- `audio_or_video`: Audio or video data
**Return Type**: String
**Example**:
```sql
SELECT TRANSCRIBE(audio_file) as transcript FROM recordings;
SELECT TRANSCRIBE(video_data) as speech_text FROM meetings;
```

### DURATION
**Syntax**: `DURATION(audio_or_video)`
**Description**: Returns duration of audio or video content
**Parameters**:
- `audio_or_video`: Audio or video data
**Return Type**: String (interval format HH:MM:SS)
**Example**:
```sql
SELECT DURATION(video_file) as length FROM videos;
SELECT * FROM recordings WHERE DURATION(audio_data) > '00:05:00';
```

### DIMENSIONS
**Syntax**: `DIMENSIONS(image_or_video)`
**Description**: Returns dimensions of image or video
**Parameters**:
- `image_or_video`: Image or video data
**Return Type**: JSON object with width and height
**Example**:
```sql
SELECT DIMENSIONS(image_data) as size FROM photos;
SELECT * FROM videos WHERE JSON_EXTRACT(DIMENSIONS(video_data), '$.width') > 1920;
```

### EXTRACT_FRAMES
**Syntax**: `EXTRACT_FRAMES(video, interval)`
**Description**: Extracts frames from video at specified intervals
**Parameters**:
- `video`: Video data
- `interval`: Time interval (string like '30 seconds' or milliseconds)
**Return Type**: Array of images
**Example**:
```sql
SELECT EXTRACT_FRAMES(video_data, '1 minute') as keyframes FROM videos;
```

### EXTRACT_AUDIO
**Syntax**: `EXTRACT_AUDIO(video)`
**Description**: Extracts audio track from video
**Parameters**:
- `video`: Video data
**Return Type**: Audio data
**Example**:
```sql
SELECT EXTRACT_AUDIO(video_file) as audio_track FROM videos;
```

### GENERATE_THUMBNAIL
**Syntax**: `GENERATE_THUMBNAIL(multimedia_data [, width, height])`
**Description**: Generates thumbnail image
**Parameters**:
- `multimedia_data`: Video, image, or other multimedia data
- `width`: Thumbnail width (default: 200)
- `height`: Thumbnail height (default: 200)
**Return Type**: Image data
**Example**:
```sql
SELECT GENERATE_THUMBNAIL(video_data, 150, 150) as thumb FROM videos;
```

### MULTIMEDIA_SIMILARITY
**Syntax**: `MULTIMEDIA_SIMILARITY(content1, content2)`
**Description**: Calculates similarity between multimedia content
**Parameters**:
- `content1`: First multimedia item
- `content2`: Second multimedia item
**Return Type**: Float64 (0.0 to 1.0)
**Example**:
```sql
SELECT MULTIMEDIA_SIMILARITY(image1, image2) as similarity FROM image_pairs;
```

### INSERT_BLOB
**Syntax**: `INSERT_BLOB(binary_data, content_type)`
**Description**: Creates multimedia data from binary content
**Parameters**:
- `binary_data`: Binary data or hex string
- `content_type`: MIME type (e.g., 'image/jpeg', 'video/mp4')
**Return Type**: Appropriate multimedia type
**Example**:
```sql
INSERT INTO media (file_data) VALUES (INSERT_BLOB(decode('FFD8FFE0...', 'hex'), 'image/jpeg'));
```

### EXTRACT_BLOB
**Syntax**: `EXTRACT_BLOB(multimedia_data)`
**Description**: Extracts binary data from multimedia content
**Parameters**:
- `multimedia_data`: Any multimedia data type
**Return Type**: Binary data
**Example**:
```sql
SELECT EXTRACT_BLOB(image_data) as raw_bytes FROM photos;
```

---

## Utility Functions

General utility functions for data manipulation and analysis.

### COALESCE
**Syntax**: `COALESCE(value1, value2, ...)`
**Description**: Returns the first non-NULL value
**Parameters**:
- `value1, value2, ...`: Values to check
**Return Type**: Same as input type
**Example**:
```sql
SELECT COALESCE(nickname, first_name, 'Unknown') as display_name FROM users;
```

### NULLIF
**Syntax**: `NULLIF(value1, value2)`
**Description**: Returns NULL if values are equal, otherwise returns first value
**Parameters**:
- `value1`: First value
- `value2`: Second value
**Return Type**: Same as first value type
**Example**:
```sql
SELECT NULLIF(score, 0) FROM test_results; -- Convert 0 to NULL
```

### CASE
**Syntax**: `CASE WHEN condition THEN result [WHEN condition THEN result] ... [ELSE result] END`
**Description**: Conditional logic
**Parameters**:
- `condition`: Boolean expression
- `result`: Value to return
**Return Type**: Varies based on result types
**Example**:
```sql
SELECT
    name,
    CASE
        WHEN age < 18 THEN 'Minor'
        WHEN age < 65 THEN 'Adult'
        ELSE 'Senior'
    END as age_group
FROM users;
```

---

## Feature Flags and Configuration

Some functions may require specific feature flags to be enabled:

- **Window Functions**: Controlled by `window_functions` feature flag
- **Statistical Functions**: Controlled by `statistical_functions` feature flag
- **Streaming SQL**: Controlled by `streaming_sql` feature flag
- **Multimodal Joins**: Controlled by `multimodal_joins` feature flag
- **NL2SQL**: Controlled by `nl2sql` feature flag
- **Vector Algebra**: Controlled by `vector_algebra` feature flag
  export AIDB_STATS_WINDOW_FUNCTIONS=true
  export AIDB_STATS_STATISTICAL_FUNCTIONS=true
  export AIDB_STATS_STREAMING_SQL=true
  export AIDB_STATS_MULTIMODAL_JOINS=true
  export AIDB_STATS_NL2SQL=true
  export AIDB_STATS_VECTOR_ALGEBRA=true

Check feature status with:
```sql
-- Check which features are enabled
SELECT * FROM SYSTEM.FEATURES;
```

---

## Performance Notes

1. **Vector Operations**: Vector similarity calculations can be computationally expensive. Consider indexing vector columns and using appropriate similarity thresholds.

2. **Multimedia Functions**: Processing large multimedia files can be resource-intensive. Consider processing in batches or using streaming operations.

3. **Statistical Functions**: Functions like MEDIAN and PERCENTILE_CONT require sorting, which can be expensive for large datasets.

4. **Window Functions**: Use appropriate PARTITION BY clauses to limit window sizes and improve performance.

5. **AI Functions**: AI function calls may involve external API calls and can have latency. Consider caching results when appropriate.

---

## Examples and Use Cases

### Time Series Analysis
```sql
-- Calculate moving averages and detect anomalies
SELECT
    timestamp,
    value,
    AVG(value) OVER (ORDER BY timestamp ROWS BETWEEN 9 PRECEDING AND CURRENT ROW) as moving_avg_10,
    STDDEV(value) OVER (ORDER BY timestamp ROWS BETWEEN 29 PRECEDING AND CURRENT ROW) as volatility,
    CASE
        WHEN ABS(value - LAG(value) OVER (ORDER BY timestamp)) >
             2 * STDDEV(value) OVER (ORDER BY timestamp ROWS BETWEEN 29 PRECEDING AND CURRENT ROW)
        THEN 'Anomaly'
        ELSE 'Normal'
    END as anomaly_flag
FROM sensor_data
ORDER BY timestamp;
```

### Semantic Search
```sql
-- Find semantically similar documents
SELECT
    title,
    content,
    embedding <=> EMBED('artificial intelligence machine learning') as similarity
FROM documents
WHERE SEMANTIC_MATCH('AI and ML technologies', content, 0.7)
ORDER BY similarity DESC
LIMIT 10;
```

### Multimedia Content Analysis
```sql
-- Analyze video content
SELECT
    video_id,
    DURATION(video_data) as length,
    DIMENSIONS(video_data) as resolution,
    TRANSCRIBE(video_data) as transcript,
    SUMMARIZE(TRANSCRIBE(video_data), 100) as summary
FROM videos
WHERE JSON_EXTRACT(DIMENSIONS(video_data), '$.width') >= 1920;
```

### Statistical Analysis
```sql
-- Comprehensive statistical analysis
SELECT
    category,
    COUNT(*) as count,
    AVG(price) as mean_price,
    MEDIAN(price) as median_price,
    STDDEV(price) as price_stddev,
    PERCENTILE_CONT(0.25, price) as q1,
    PERCENTILE_CONT(0.75, price) as q3,
    MIN(price) as min_price,
    MAX(price) as max_price
FROM products
GROUP BY category
ORDER BY mean_price DESC;
```

This reference covers all major SQL functions implemented in AIDB. For the most up-to-date information and additional functions, consult the official AIDB documentation and release notes.