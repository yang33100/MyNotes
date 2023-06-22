# 数据结构

## ArrayList
```c#
本质是一个object类型的数组类

using System.Collections

//申明
ArrayList array = new ArrayList(capacity容量大小);

array.Count //长度
array.capacity //容量

//增加
array.Add(任意类型)
array.AddRange(ArrayList类型)

//插入指定位置
array.Insert(index,元素值)

//删除从左到右第一个匹配的元素
array.Remove(元素值)

//移出指定位置元素
array.RemoveAt(index)

//清空
array.Clear()

//判断是否存在该值
array.Contains(元素值)

//正向查找返回index 找不到返回-1
array.IndexOf(元素值)

//反向查找返回index 找不到返回-1
array.LastIndexOf(元素值);

//使用指定的比较器在已排序 ArrayList 的某个元素范围中搜索元素，并返回该元素从零开始的索引。 L,R范围和cmp可选
array.BinarySearch(Int32, Int32, Object, IComparer)

//L R cmp可选  快排 平均O nlogn
array.Sort(Int32, Int32, IComparer)

//遍历
for(int i = 0; i < array.Count; i ++)

foreach (object item in array)

//装箱拆箱
值类型存储会装箱，取出值类型会拆箱
```
![Alt text](image-14.png)

## Stack
```c#
命名空间 System.Collections
object类型数组

Stack stk = new Stack();

stk.Push(值);

//返回出栈值
stk.Pop();

//栈顶元素
stk.Peek()

//是否存在该值
stk.Contains(元素值)

stk.Clear()

stk.Count() //长度

//从栈顶到底
foreach (object it in stk)
{}

//强转成object数组 也是从顶到底的顺序
object[] arr = stack.ToArray();
for(int i = 0; i < arr.Length; i ++)

while( stack.Count > 0)
{
    object o = stack.Pop();
    //使用o
}

存在装箱拆箱
```

## Queue
```c#
Queue q = new Queue();

q.Enqueue(元素)

//返回取出的队头元素
q.Dequeue()

//队头元素
q.Peek()

q.Contains(元素)

q.Clear()

装箱拆箱
```

## HashTable 类c++的map
```c#
Hashtable hash = new Hashtable()

hash.Add(key , value);

hash.Remove(key)

hash.Clear()

//返回value 找不到返回null
hash[key]

hash.Contains(key)
hash.ContainsKey(key)
hash.ContainsValue(value)

//修改
hash[xx] = 3;

//对数
hash.Count()

//遍历键
foreach (object it in hash.Keys)
//遍历值
foreach (object it in hash.Values)

//遍历key value 对
foreach (DictionaryEntry it in hash)
{
    it.Key
    it.Value
}

//迭代器
IDictionaryEnumerator myEnumerator = hash.GetEnumerator();
bool flag = myEnumerator.MoveNext();
while(flag)
{
    myEnumerator.Key
    myEnumerator.Value
    flag = myEnumerator.MoveNext();
}

//装箱拆箱
```

