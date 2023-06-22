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

## HashTable
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

# 泛型
## 泛型知识点
![Alt text](image-15.png)
![Alt text](image-16.png)
```c#
class Test<T>
{
    public T value;
}
class Test2<T,P>
{
    public T value1;
    public P value1;
}

Test<int> t = new Test<int>();
Test2<int,string> t2 = new Test2<int,string>();
```
![Alt text](image-17.png)
![Alt text](image-18.png)

```c#
作用：
1.不同类型对象的相同逻辑处理可以选择泛型
2.使用泛型可以一定程度避免装箱拆箱
```

## 泛型约束
![Alt text](image-19.png)
```c#
//例
class Test1<T> where T:struct
{
    public T value;
    public void TestFun<K>() where K:struct
    {

    }
}

//可以组合约束

//多个泛型有约束
class Test<T, K> where T:class,new() where K:struct
{

}

//用泛型实现一个单例模式基类(有缺点：可以new)
class SingleInstanceBase<T> where T : new()
{
    private static T instance = new T();

    public static T Instance
    { get {  return instance; } }
}
```
# 泛型数据结构
## List
```c#
本质：可变类型的泛型数组
using System.Collections.Generic

List<int> list1 = new List<int>();
List<int> list2 = new List<int>();
List<string> list3 = new List<string>();

list1.Add(3);
list2.Add(1);
list1.AddRange(list2);
list1.Insert(1,2);
list1.Remove(3);
list2.RemoveAt(0);
list1.Clear();

list[index] = xxx;

list.Contains(元素)

list.IndexOf(index)
list.LastIndexOf(index)

list.Count
list.Capacity

for(int i = 0; i < list.Count; i ++ )
{
    //list[i]
}

foreach (int it in list)
{
    //it
}
```

## Dictionary 类c++的map
```c#
using System.Collections.Generic

Dictionary<int,int> dic = new Dictionary<int,int>();

dic.Add(1,2);
dic[1] = 5;
dic.Remove(key)
dic.Clear();
//后略 参照HashTable

foreach (KeyValuePair<int,int> it in dic)
{
    it.Key
    it.Value
}
```

## LinkedList
```c#
可变类型的泛型双向链表

LinkedList<int> linkedList = new LinkedList<int>();


AddLast(元素)
AddFirst(元素)

//适合和Find共用
AddAfter(LinkedListNode,元素值) //插入在LinkedListNode类型值的后面
AddBefore(LinkedListNode,元素值)

RemoveFirst()
RemoveLast()
Remove(元素)
Clear()

//返回头结点 尾结点同
LinkedListNode<int> first = linkedList.First;

//返回节点LinkedListNode
Find(元素)

Contains(元素)

LinkedListNode.value = xxx;

//遍历
foreach (int it in linkedList)
{
    //it为值
}

LinkedListNode<int> p = linkedList.First;
while(p != null)
{
    //p.value
    p = p.Next; 
}

LinkedListNode<int> p = linkedList.Last;
while(p != null)
{
    //p.value
    p = p.Previous; 
}

```

## Stack<> Queue<>
```
泛型栈 泛型队列
```

# 委托和事件
## 委托
```c#
//概念
委托是 函数(方法) 的容器
可以理解为表示 函数(方法) 的变量类型
用来存储、传递 函数(方法)
委托的本质是一个类，用来定义 函数(方法) 的类型(返回值和参数的类型)
不同的 函数(方法) 必须对应和各自"格式"一致的委托
//委托支持泛型

关键字：delegate
语法：
//访问修饰符不写默认为public（可以在别的命名空间访问）
//同一语句块中委托名不能重名
访问修饰符 delegate 返回值 委托名(参数列表);

可以申明在namespace和class中


//定义和使用自定义委托
//无参无返回值
delegate void MyFun();//申明了一个可以用来存储无参无返回值函数的容器
static void Fun(){}
//f装载了Fun函数
MyFun f = new Myfun(Fun); //相同写法:MyFun f = Fun;
f.Invoke(); // 调用执行
f() // 执行第二种写法

//有参有返回值
delegate int F(int x);
static int Fun1(int x){}
F f1 = Fun1; //F f1 = new F(Fun1)
f1(1); // f1.Invoke(1)

委托变量是函数的容器
委托常用在：
1.作为类的成员
2.作为函数的参数

class Test
{
    public MyFun myFun;

    public Test(MyFun f1,MyFun f2)
    {
        this.myFun = f1;
        f2();
    }
}

//用委托存储多个函数 多播委托
MyFun f = null;
f += Fun;
f += Fun;
f(); //执行两次Fun()
f -= Fun; //多减不会报错，不处理
f(); //执行1次

//系统定义好的委托 Action无返回值，Func有返回值
//无参      无返回值
System.Action act = Fun;
act += Fun;
act();

//可以传多个参数的(最多支持16个) 无返回值
System.Action<参数类型1,参数类型2，...，参数类型16> act;

//无参    有泛型返回值
System.Func<返回值类型> fc = MyFunReturnString;

//可以传多个参数的(最多支持16个) 有泛型返回值的
System.Func<参数类型1,...,参数类型16，返回类型> fc;

```