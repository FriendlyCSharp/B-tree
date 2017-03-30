# [FriendlyCSharp.Databases](https://github.com/FriendlyCSharp/Databases)

A library of cross platform C# data structures. Generic [**B-tree**](https://en.wikipedia.org/wiki/B-tree) written in C#, which can be replaced with NoSQL database stored in the memory of discharge requirements in real-time (*Firebase, Redis Cache, SAP HANA, Exadata, OLTP, etc.*). Basic information B-tree can be found in the book N. Wirth, Algorithms + data structures = programs and on Wikipedia, namely:
>"*In computer science, a B-tree is a self-balancing tree data structure that keeps data sorted and allows searches, sequential access, insertions, and deletions in logarithmic time. The B-tree is a generalization of a binary search tree in that a node can have more than two children (Comer 1979, p. 123). Unlike self-balancing binary search trees, the B-tree is optimized for systems that read and write large blocks of data. B-trees are a good example of a data structure for external memory. It is commonly used in databases and filesystems. (...) Rudolf Bayer and Ed McCreight invented the B-tree while working at Boeing Research Labs in 1971 (Bayer & McCreight 1972), but they did not explain what, if anything, the B stands for.*" -&nbsp;[Wikipedia](https://en.wikipedia.org/wiki/B-tree).

&nbsp;
## B-Tree generic class
#### [FcsBTreeN&lt;TKey, TValue&gt;](FcsBTreeN.cs)
   + `Methods:` BtnCompares, BtnUpdates, BtnAdd, BtnDeleteAll, BtnFind, BtnFirst, BtnLast, BtnNext, BtnPrev, BtnSearch, BtnSearchPrev, BtnUpdate and BtnUsedKeys.
#### [FcsFastBTreeN&lt;TKey, TValue&gt;](FcsFastBTreeN.cs)
   + `Methods:` BtnCompares, BtnUpdates, BtnAdd, BtnDeleteAll, BtnFind, BtnFirst, BtnLast, BtnNext, BtnPrev, BtnSearch, BtnSearchPrev, BtnUpdate and BtnUsedKeys.
   + `Methods:` BtnFastFind, BtnFastFirst, BtnFastLast, BtnFastNext, BtnFastPrev, BtnFastSearch, BtnFastSearchPrev.
#### [FcsLockBTreeN&lt;TKey, TValue&gt;](FcsLockBTreeN.cs)
   + `Methods:` BtnCompares, BtnUpdates, BtnAdd, BtnDeleteAll, BtnFind, BtnFirst, BtnLast, BtnNext, BtnPrev, BtnSearch, BtnSearchPrev, BtnUpdate and BtnUsedKeys.
#### [FcsFastLockBTreeN&lt;TKey, TValue&gt;](FcsFastLockBTreeN.cs)
   + `Methods:` BtnCompares, BtnUpdates, BtnAdd, BtnDeleteAll, BtnFind, BtnFirst, BtnLast, BtnNext, BtnPrev, BtnSearch, BtnSearchPrev, BtnUpdate and BtnUsedKeys.
   + `Methods:` BtnFastFind, BtnFastFirst, BtnFastLast, BtnFastNext, BtnFastPrev, BtnFastSearch, BtnFastSearchPrev.

&nbsp;
## Performance
A [**B-tree**](https://en.wikipedia.org/wiki/B-tree) of order m is a tree which satisfies the following properties:
1. Every node has at most m children.
2. Every non-leaf node (except root) has at least ⌈m/2⌉ children.
3. The root has at least two children if it is not a leaf node.
4. A non-leaf node with k children contains k−1 keys.
5. All leaves appear in the same level.

| generic class | sorted by&nbsp;key | duplicate keys | B-tree | locking records |
| --- | :---: | :---: | :---: | :---: |
| [**fastDB&lt;...&gt;**](http://www.inmem.cz/inmem_letak.pdf) | **Yes** | **Yes** | **Yes** | **Yes** |
| [**FcsBTreeN&lt;TKey, TValue&gt;**](#fcsbtreentkey-tvalue) | **Yes** | **Yes** | **Yes** | No |
| [**FcsFastBTreeN&lt;TKey, TValue&gt;**](#fcsfastbtreentkey-tvalue) | **Yes** | **Yes** | **Yes** | No |	
| [**FcsLockBTreeN&lt;TKey, TValue&gt;**](#fcslockbtreentkey-tvalue) | **Yes** | **Yes** | **Yes** | No |
| [**FcsFastLockBTreeN&lt;TKey, TValue&gt;**](#fcsfastlockbtreentkey-tvalue) | **Yes** | **Yes** | **Yes** | No |
| SortedSet&lt;KeyValuePair&lt;TKey, TValue&gt;&gt; | **Yes** | No | No | No |
| HashSet&lt;KeyValuePair&lt;TKey, TValue&gt;&gt; | No | No | No | No |
| Dictionary&lt;TKey, TValue&gt; | No | No | No | No |

&nbsp;
## Benchmark 
The benchmark was configured as follows:
* CPU: Intel Xeon E3-1245 @ 3.3 GHz;
* Windows 10, 64bit, .NET Standard 1.2

>**Adding in a single thread:**

| &lt;int, uint&gt; | sorted by&nbsp;key | iteration | total&nbsp;(ms) | one time (ns) | speed | RAM&nbsp;(MB) | occupied |
| --- | :---: | ---: | ---: | ---: | :---: | :---: | :---: |
| [**FcsFastBTreeN&lt;...&gt;**](#fcsfastbtreentkey-tvalue) | **Yes** | 10,000,000 | **6,185** | **619** | **100%** | **128** | **100%** |
| SortedSet&lt;...&gt; | **Yes** | 10,000,000 | ~~&nbsp;19,443&nbsp;~~ | ~~&nbsp;1,944&nbsp;~~ | ~~&nbsp;32%&nbsp;~~ | ~~&nbsp;458&nbsp;~~ | ~~&nbsp;358%&nbsp;~~ |
| HashSet&lt;...&gt; | No | 10,000,000 | 2,017 | 202 | 307% | 229 | 179% |
| Dictionary&lt;...&gt; | No | 10,000,000 | 1,378 | 138 | 449% | 229 | 179% |

>**Foreach in a single thread:**

| &lt;int, uint&gt; | sorted by&nbsp;key | iteration | total&nbsp;(ms) | one time&nbsp;(ns) | speed |
| --- | :---: | ---: | ---: | ---: | :---: |
| [**fastDB&lt;...&gt;**](http://www.inmem.cz/inmem_letak.pdf) | **Yes** | 10,000,000 | **101** | **10.08** | **198%** |		
| [**FcsFastBTreeN&lt;...&gt;**](#fcsfastbtreentkey-tvalue) | **Yes** | 10,000,000 | **200** | **20** | **100%** |		
| SortedSet&lt;...&gt; | **Yes** | 10,000,000 | ~~&nbsp;1,230&nbsp;~~ | ~~&nbsp;123&nbsp;~~ | ~~&nbsp;16%&nbsp;~~ |
| HashSet&lt;...&gt; | No | 10,000,000 | 47.3 | 4,73 | 422%	|
| Dictionary&lt;...&gt; | No | 10,000,000 | 86.5 | 8,65 | 231% |		

　
## Install
Install via Nuget Package Manager

```
PM> Install-Package FriendlyCSharp.Databases
```

## LICENSE
See the [LICENSE](LICENSE).
