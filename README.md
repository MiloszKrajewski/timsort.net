# timsort.net

*This implementation is a C# translation of Josh Bloch's Java implementation of TimSort.*

## Links
* [Wikipedia](http://en.wikipedia.org/wiki/Timsort)
* Josh Bloch's [Java implementation](http://gee.cs.oswego.edu/cgi-bin/viewcvs.cgi/jsr166/src/main/java/util/TimSort.java?view=co)

## Description

TimSort takes advantage of two facts:
* data we sort is often already partially sorted
* comparison might be expensive (complex Compare method) while swapping elements is cheap (swapping pointers)

When comparison gets slower (for example, comparing complex objects) TimSort increases its advantage over QuickSort.

*NOTE*: "Partially sorted data" in cases below mean that data is generated with 80% chance that next item is greater/smaller than previous one.

### Array of 5368709 items, quick compare function (int.CompareTo(int))

|            | Built-in    | TimSort     |
|------------|-------------|-------------|
| Random     | 1859.4927ms | 1773.2582ms |
| Ascending  | 1166.6400ms |  247.1780ms |
| Descending | 1190.5521ms |  571.7132ms |

*NOTE:* TimSort's performance is the same for random data, but is significantly better for already ordered data.

### Array of 536870 items, quite slow compare function (I actually added Thread.Sleep(0) to it)

|            | Built-in    | TimSort     |
|------------|-------------|-------------|
| Random     | 6117.1032ms | 4578.1129ms |
| Ascending  | 5323.7977ms |  841.0910ms |
| Descending | 5321.9103ms | 1094.5267ms |

*NOTE:* TimSort's performance is better than QuickSort's when compare function is slow, even for random data.
