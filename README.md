# timsort.net

*NOTE:*: the documentation below is copy-paste from CodePlex which is using different flavour of Markdown. I'll clean it up soon.
---

*This implementation is a C# translation of Josh Bloch's Java implementation of TimSort.*

Wikipedia: 
[url:http://en.wikipedia.org/wiki/Timsort]
Josh Bloch's Java implementation: 
[url:http://gee.cs.oswego.edu/cgi-bin/viewcvs.cgi/jsr166/src/main/java/util/TimSort.java?view=co]

TimSort takes advantage of two facts:
* data we sort is often already partially sorted
* comparison might be expensive (complex Compare method) while swapping elements is cheap (swapping pointers)
When comparison gets slower (for example, comparing complex objects) TimSort increases its advantage over QuickSort.

*Array of 5368709 items, quick compare function: (actually: int.CompareTo(int))*
* Random data
** Builtin: 1859.4927ms
** TimSort: 1773.2582ms
* Generally ascending data (80% chance that next item is greater than previous one)
** Builtin: 1166.6400ms;
** TimSort: 247.1780ms
* Generally descending data (80% chance that next item is smaller than previous one)
** Builtin: 1190.5521ms
** TimSort: 571.7132ms
*NOTE:* TimSort's performance is the same for random data, but is significantly better for already ordered data.

*Array of 536870 items, quite slow compare function (I actually added Thread.Sleep(0) to it):*
* Random data
** Builtin: 6117.1032ms
** TimSort: 4578.1129ms
* Generally ascending data (80% chance that next item is greater than previous one)
** Builtin: 5323.7977ms
** TimSort: 841.0910ms
* Generally descending data (80% chance that next item is smaller than previous one)
** Builtin: 5321.9103ms
** TimSort: 1094.5267ms
*NOTE:* TimSort's performance is better than QuickSort's when compare function is slow, even for random data.
