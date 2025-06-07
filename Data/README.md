# Data
- [Minimum number of workers on Spark](#minimum_number_of_workers_on_spark)

## Minimum number of workers on Spark <a name="minimum_number_of_workers_on_spark"></a>
PySpark can run without separate workers, but only in local mode, where the driver executes all tasks by itself.
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .master("local[*]") \  # "*" means use all accessible threads
    .appName("My app") \
    .getOrCreate()

```