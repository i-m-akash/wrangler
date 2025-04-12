**##📦 Byte Size & Time Duration Parsers with aggregate-stats Directive**

This enhancement adds native support for parsing byte size and time duration units in CDAP Wrangler, along with a new directive called aggregate-stats that can compute total/average values across records.

---

## ✨ Features

### ✅ New Token Types

- Byte Size Units Supported:  
  B, KB, MB, GB, TB, PB, KiB, MiB, GiB

- Time Duration Units Supported:  
  ms, s, sec, m, min, h

These tokens are now fully supported as directive arguments.

---

## 🧠 Usage Example

```wrangler
aggregate-stats :data_transfer_size :response_time total_size_mb total_time_sec
```

| Parameter            | Description                                                  |
|---------------------|--------------------------------------------------------------|
| :data_transfer_size | Column with byte size values (e.g., "10MB", "512KiB")         |
| :response_time      | Column with duration values (e.g., "150ms", "2.1s", "1min")   |
| total_size_mb       | Output column: total size (converted to MB)                   |
| total_time_sec      | Output column: total time (converted to seconds)              |

---

## 🧮 Units Conversion

### Byte Size Conversion Table

| Unit | Multiplier      |
|------|-----------------|
| B    | 1               |
| KB   | 1,000           |
| MB   | 1,000,000       |
| GB   | 1,000,000,000   |
| TB   | 1,000,000,000,000 |
| PB   | 1,000,000,000,000,000 |
| KiB  | 1,024           |
| MiB  | 1,048,576       |
| GiB  | 1,073,741,824   |

### Time Duration Conversion Table

| Unit  | Multiplier (to ms) |
|-------|---------------------|
| ms    | 1                   |
| s/sec | 1,000               |
| m/min | 60,000              |
| h     | 3,600,000           |

---

## 🧪 Test Coverage

✅ Unit Tests Included:

- ByteSizeTest.java — Validates parsing and conversion of byte size strings  
- TimeDurationTest.java — Validates parsing and conversion of time duration strings  
- AggregateStatsTest.java — End-to-end test validating correct aggregation output

---

## 📁 File Structure

```
wrangler-api/
└── parser/
    ├── ByteSize.java
    ├── TimeDuration.java
    └── TokenType.java

wrangler-core/
├── src/main/antlr4/io/cdap/wrangler/parser/Directives.g4
├── parser/RecipeVisitor.java
└── plugin/AggregateStats.java

wrangler-core/
└── src/test/java/
    ├── ByteSizeTest.java
    ├── TimeDurationTest.java
    └── AggregateStatsTest.java
```

---

## 🤖 AI Assistance Log

Development of this feature included assistance via large language models. Prompts and responses are recorded in prompts.txt.

---

## 🚀 Build Instructions

Use Maven to build the project:

```bash
mvn clean install
```

---

## ✅ Sample Output

Given Input:

| data_transfer_size | response_time |
|--------------------|---------------|
| 10MB               | 150ms         |
| 5MB                | 2.1s          |

After Running aggregate-stats:

| total_size_mb | total_time_sec |
|---------------|----------------|
| 15.0          | 2.25           |


