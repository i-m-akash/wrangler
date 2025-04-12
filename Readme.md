Byte Size & Time Duration Parsers with aggregate-stats Directive
This enhancement adds native support for parsing byte size and time duration units in CDAP Wrangler, along with a new directive called aggregate-stats that can compute total/average values across records.

✨ Features
✅ New Token Types
Byte Size Units Supported: B, KB, MB, GB, TB, PB, KiB, MiB, GiB


Time Duration Units Supported: ms, s, sec, m, min, h


These tokens can now be used directly in directive arguments.

🧠 Usage Example
aggregate-stats :data_transfer_size :response_time total_size_mb total_time_sec

Parameter
Description
:data_transfer_size
Source column containing byte size values (e.g. 10MB)
:response_time
Source column containing duration values (e.g. 150ms)
total_size_mb
Output column name for total size in MB
total_time_sec
Output column name for total time in seconds


🧮 Units Conversion
ByteSize Conversion Table
Unit
Multiplier
B
1
KB
1,000
MB
1,000,000
GB
1,000,000,000
TB
1,000,000,000,000
PB
1,000,000,000,000,000

TimeDuration Conversion Table
Unit
Multiplier (to ms)
ms
1
s/sec
1,000
m/min
60,000
h
3,600,000


🧪 Test Coverage
✅ Unit Tests
ByteSizeTest.java – Validates parsing and conversion of byte size strings.


TimeDurationTest.java – Validates parsing and conversion of time duration strings.


AggregateStatsTest.java – End-to-end test verifying correct aggregation results.



📁 File Structure
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
└── src/test/java/...
    ├── ByteSizeTest.java
    ├── TimeDurationTest.java
    └── AggregateStatsTest.java


🤖 AI Assistance Log
Prompts used during development are recorded in prompts.txt in the root directory.

🚀 How to Build
mvn clean install


✅ Sample Output
Given a dataset:
data_transfer_size
response_time
10MB
150ms
5MB
2.1s

Output after aggregate-stats:
total_size_mb
total_time_sec
15.0
2.25

