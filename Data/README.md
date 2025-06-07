# Data
- [Cache in PySpark](#cache_in_pyspark)
- [`collect()` in PySpark](#collect_in_pyspark)
- [`count()` in PySpark](#count_in_pyspark)
- [Data shuffeling](#data_shuffling)
- [Minimum number of workers on Spark](#minimum_number_of_workers_on_spark)
- [Narrow vs wide transformation in Spark](#narrow_vs_wide_transformation_in_spark)
- [TempView in PySpark](#tempview_in_pyspark)

## Cache in PySpark <a name="cache_in_pyspark"></a>
- `df.cache()` - is a shortcut for `df.persist(StorageLevel.MEMORY_AND_DISK)`. The worker will try to store the data in RAM, and if it doesn't fit, it will save the remaining data to disk.
- `df.persist()` - allows you to specify exactly how and where the data should be stored (RAM only, RAM + disk, disk only).

## `collect()` in PySpark <a name="collect_in_pyspark"></a>
It returns all the data.

## `count()` in PySpark <a name="count_in_pyspark"></a>
It returns the number of all rows in the DataFrame.

## Data shuffeling <a name="data_shuffling"></a>
Data shuffling is the process of transferring data between partitions or cluster nodes. It occurs during wide transformations, such as `join`, `reduceByKey`, or `groupByKey`, which require rearranging data so that elements with the same keys end up in the same partition.

## Minimum number of workers on Spark <a name="minimum_number_of_workers_on_spark"></a>
PySpark can run without separate workers, but only in local mode, where the driver executes all tasks by itself.
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .master("local[*]") \  # "*" means use all accessible threads
    .appName("My app") \
    .getOrCreate()

```

## Narrow vs wide transformation in Spark <a name="narrow_vs_wide_transformation_in_spark"></a>
- Narrow transformations do not require data shuffling because each input partition maps to only one output partition. Examples include `map()` and `filter()`.
- Wide transformations require data shuffling, as data is redistributed across partitions. Examples include `reduceByKey()` and `join()`.

## TempView in PySpark <a name="tempview_in_pyspark"></a>
TempView is a temporary, abstract representation of a DataFrame as an SQL table, allowing you to run SQL queries directly on the data stored in the DataFrame. It does not create a new physical table nor copies the data.