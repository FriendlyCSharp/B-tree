# FriendlyCSharp.Databases

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

&nbsp;
## Functions
Various methods used throughout the library.

### Comparator
Some data structures require a comparator method to automatically keep their elements sorted upon insertion. 

>Default comparator is initialized as follows:

```cs
protected virtual int BtnCompares(TKey keyX, TKey keyY, object objCmp)
{
  return keyX.CompareTo(keyY);
}
```

>**Writing custom class with comparators is easy:**

```cs
public class MyBtnKeyValue : FcsBTreeN<int, uint>
{
  protected override void BtnUpdates(int keyAdd, uint valueAdd, ref uint valueUpdates, object objUpdates)
  {
    valueUpdates++;
  }
  //////////////////////////
  protected override int BtnCompares(int keyX, int keyY, object objCmp)
  {
    return keyX - keyY;
  }
  //////////////////////////
  public MyBtnKeyValue() : base()
  {
  }
}
```

### Iterators

All ordered containers have stateful iterators. Typically an iterator is obtained by _Iterator()_ function of an ordered container. Once obtained, iterator''s _Next()_ function moves the iterator to the next element and returns true if there was a next element. If there was an element, then element''s can be obtained by iterator''s _Value()_ function. Depending on the ordering type, it''s position can be obtained by iterator''s _Key()_ functions. Some containers even provide reversible iterators, essentially the same, but provide another extra _Prev()_ function that moves the iterator to the previous element and returns true if there was a previous element.Note: it is unsafe to remove elements from container while iterating.

#### Iterator

Tree gradually passes from the lowest, from the specified keys or higher.

>Typical usage:

```cs
foreach(KeyValuePair<int, uint>? BtnKV in MyBtnKeyValue)
{
}
```

>Other usages:

```cs
if (MyBtnKeyValue.BtnFirst(out btnKey, out btnValue) != null)
{
  do
  {
  }
  while (MyBtnKeyValue.BtnNext(ref btnKey, out btnValue) != null)
}
```

```cs
if (MyBtnKeyValue.BtnFind(btnKey, out btnValue) != null)
{
  do
  {
  }
  while (MyBtnKeyValue.BtnNext(ref btnKey, out btnValue) != null)
}
```

```cs
if (MyBtnKeyValue.BtnSearch(ref btnKey, out btnValue) != null)
{
  do
  {
  }
  while (MyBtnKeyValue.BtnNext(ref btnKey, out btnValue) != null)
}
```

#### Reverse Iterator

The tree passes successively from the last or entered or lower than the specified key.

>Typical usage of iteration in reverse:

```cs
if (MyBtnKeyValue.BtnLast(out btnKey, out btnValue) != null)
{
  do
  {
  }
  while (MyBtnKeyValue.BtnPrev(ref btnKey, out btnValue) != null)
}
```

>Other usages:

```cs
if (MyBtnKeyValue.BtnFind(btnKey, out btnValue) != null)
{
  do
  {
  }
  while (MyBtnKeyValue.BtnPrev(ref btnKey, out btnValue) != null)
}
```

```cs
if (MyBtnKeyValue.BtnSearchPrev(btnKey, out btnValue) != null)
{
  do
  {
  }
  while (MyBtnKeyValue.BtnPrev(ref btnKey, out btnValue) != null)
}
```

### Enumerate

Methods that seek the desired key and returns the key value pair or null.

>**Find**

The method finds the specified key and returns the key value pair or null.

```cs
public virtual  bool? BtnFind(TKey key, out TValue value)
{
}
public virtual (TKey key, TValue value)? BtnFind(TKey key)
{
}
```

>**First**

The method finds the first key and returns the key value pair or null.

```cs
public virtual bool? BtnFirst(out TKey key, out TValue value)
{
}
public virtual (TKey key, TValue value)? BtnFirst()
{
}
```

>**Last**

The method finds the last key and returns the key value pair or null.

```cs
public virtual bool? BtnLast(out TKey key, out TValue value)
{
}
public virtual (TKey key, TValue value)? BtnLast()
{
}
```

>**Search**

The method finds the specified key or the next higher and returns the key value pair or null.

```cs
public virtual bool? BtnSearch(ref TKey key, out TValue value)
{
}
public virtual (TKey key, TValue value)? BtnSearch(TKey key)
{
}
```

>**SearchPrev**

The method finds the specified key or the next lower and returns the key value pair or null.

```cs
public virtual bool? BtnSearchPrev(ref TKey key, out TValue value)
{
}
public virtual (TKey key, TValue value)? BtnSearchPrev(TKey key)
{
}
```

>**Example:**

```cs
```
　
## Install
Install via Nuget Package Manager

```
PM> Install-Package FriendlyCSharp.Databases
```

## LICENSE
See the [LICENSE](LICENSE).
