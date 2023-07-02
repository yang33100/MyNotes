# C#入门
## 注释
``` c#
// 单行注释
/*
    多行注释
*/

/// 命名空间、类等的三杠注释，为后续编译器提示提供写的注释内容
```
## 输入输出语句
``` c#
//打印自动加空行
Console.WriteLine("hello world");
//打印无空行
Console.Write("你好\n123 456\n");
//读入一行
Console.ReadLine();
//读到任意键
Console.ReadKey();
//Console.ReadKey(true) 加上true不会把输入内容显示在控制台
//.keychar 获得读入的char
```
## 折叠代码
``` c#
#region 标题
//此处代码可折叠
#endregion
```
## 变量类型
### 有符号整形
``` C#
sbyte : -128 ~ 127, 1 byte
short : -32768 ~ 32767, 2 byte
int : -2e9 ~ 2e9, 4 byte
long : -9e18 ~ 9e18, 8 byte
```
### 无符号整形
``` C#
byte : 0 ~ 255
ushort : 0 ~ 65535
uint : 0 ~ 4e9
ulong : 0 ~ 1.8e19
```
### 浮点数
``` C#
默认小数为double类型
float : 7位精度, f, 4 byte
double : 15~16位, 8 byte
decimal ： 27~28位, m, 16 byte
```
### 其他类型
``` c#
bool : true / false 1 byte
char : 字符 2 byte
string : 字符串
```
## 命名规范
``` c#
//变量，首字母小写，后单词首字母大写 驼峰命名法
string myName = "xx"; 
//函数、类 均首字母大写 帕斯卡命名法
string MyName = "xx";
```
## 常量
```
1.必须被初始化
2.不能被修改
```
## 转义字符
``` c#
\n 回车
\t tab
\a 警告音
@"字符串" @：取消转义
```

## 隐式转换
```
float和double不能隐式转成decimal
bool不能用数字表示
其他类似规则
```
## 显示转换
```
1.括号强转：
(强转类型) 原类型

2.parse方法：
作用：将string转化成对应类型
语法：变量类型.Parse("字符串")
范围不够会报错

3.Convert类
作用：各个类型相互转换，会四舍五入
语法：Convert.To类型名(变量名)
可转bool，true=1 false=0

4.toString()方法
变量.toString()
```

## 异常捕获
``` c#
try
{
    //执行代码
}
catch(Exception e)
{
    //报错后执行
}
finally // 可选
{
    //不管出错都会执行
}
```

## 运算符
``` c#
+ - * / % 
+= -= *= /= %=
++ --
< <= > >= != ==
&& || !
& | ^ << >> ~
?: 
同C语言
```

## 字符串拼接
```c#
1.用+拼接 也可用+=
str = "123";
str += "" + 1 + 2; // 12312
str += 1 + 2； //123123

2. string.Format("我是{0},{1}","syy","你好",...)

3.控制台打印
Console.WriteLine("我是{0},{1}","syy","你好",...)
Write方法同上
```

### if,switch,for,while均与c语言相同

## 控制台相关
```c#
//1.清空
Console.Clear();

/*2.设置控制台大小
    窗口大小   缓冲区大小
    先设置窗口大小 再设置缓冲区大小
    
    限制:
    缓冲区大小 >= 窗口大小
    窗口大小 <= 控制台最大尺寸
*/
// 窗口大小
Console.SetWindowSize(100,50);
// 缓冲区大小
Console.SetBufferSize(100,1000);

/*3.设置光标位置
  控制台左上角为坐标原点
   0-----> x轴
   |
   |
   ↓
   y轴

   限制：坐标 <= 缓冲区大小
*/
//横纵距离单位不同，1y = 2x （视觉上）
Console.SetCursorPosition(10,5);

// 4.设置颜色

// 文字颜色
Console.ForeGroundColor = ConsoleColor.Red;

// 背景颜色
Console.BackgroundColor = ConsoleColor.Blue;
Console.Clear();//需要clear才能全屏染色

// 5.光标可见
Console.CursorVisible = false;

// 6.关闭控制台
Environment.Exit(0);
```
### 作业代码
``` c#
/*
    控制黄色方块wasd在红色背景控制台移动
*/
Console.BackgroundColor = ConsoleColor.Red;
Console.Clear();
Console.CursorVisible = false;
Console.ForegroundColor = ConsoleColor.Yellow;
Console.Write('■');
int x=0, y=0;
while(true)
{
    Console.SetCursorPosition(x, y);
    Console.Write('■');

    char c = Console.ReadKey(true).KeyChar;
    
    //覆写 也可以用clear 但 clear会闪烁
    Console.SetCursorPosition(x, y);
    Console.Write("  ");
 
    switch (c)
    {
        //贯穿
        case 'W':
        case 'w':
            if (y >= 1) --y;
            break;

        case 'A':
        case 'a':
            if (x >= 2) x-=2;
            break;
        case 'S':
        case 's':
            if (y+1 < Console.BufferHeight) ++y;
            break;
        case 'D':
        case 'd':
            if (x+2 < Console.BufferWidth) x+=2;
            break;
    }
    
}
```

## 随机数
```c#
//范围左开右闭
Random rd = new Random();

int i = rd.Next(); // 生成一个非负数的随机数

i = Next(100); // 0~99

i = Next(5,100) // 5~99
```
## 入门实践 控制台项目--勇者救公主
```
#region 窗口设置
int w = 50, h = 30;
Console.SetWindowSize(w, h);
Console.SetBufferSize(w, h);
Console.CursorVisible = false;
#endregion

#region 场景属性
int sceneId = 0;
int sceneIdNum = 3;
#endregion

#region 状态设置
int selectId0 = 0;
int selectId0Num = 2;
#endregion
String endMessage = "";
Random random = new Random();

while (true)
{
    switch (sceneId)
    {
        //开始界面
        case 0:
            Console.Clear();
            Console.SetCursorPosition(w / 2 - 6, 6);
            Console.ForegroundColor = ConsoleColor.White;
            Console.Write("勇者智斗恶龙");
            Console.SetCursorPosition(w / 2 - 4, 10);
            Console.ForegroundColor = selectId0 == 0 ? ConsoleColor.Red : ConsoleColor.White;
            Console.Write("开始游戏");
            Console.SetCursorPosition(w / 2 - 4, 14);
            Console.ForegroundColor = selectId0 == 1 ? ConsoleColor.Red : ConsoleColor.White;
            Console.Write("退出游戏");
            char getKey = Console.ReadKey(true).KeyChar;
            if (getKey == 'w' || getKey == 'W')
            {
                selectId0 = (selectId0 - 1 + selectId0Num) % selectId0Num;
            }
            else if (getKey == 'S' || getKey == 's')
            {
                selectId0 = (selectId0 + 1) % selectId0Num;
            }
            else if (getKey == 'j' || getKey == 'J')
            {
                if (selectId0 == 0) sceneId++;
                else Environment.Exit(0);
            }
            break;
        //游戏界面
        case 1:
            Console.Clear();
            #region 设置边界
            Console.ForegroundColor = ConsoleColor.Red;
            for (int i = 0; i <= w - 2; i ++ )
            {
                Console.SetCursorPosition(i, 0);
                Console.Write('■');
                Console.SetCursorPosition(i, h - 7);
                Console.Write('■');
                Console.SetCursorPosition(i, h - 1);
                Console.Write('■');
            }
            for (int i = 0; i < h; i ++ )
            {
                Console.SetCursorPosition(0, i);
                Console.Write('■');
                Console.SetCursorPosition(w - 2, i);
                Console.Write('■');
            }
            #endregion
            #region 勇者属性
            int playerX = 2;
            int playerY = 1;
            int playerAtkMin = 7;
            int playerAtkMax = 14;
            int playerHp = 100;
            int playerDx = 1;
            int playerDy = 0;
            bool isFight = false;
            bool isOver = false;
            #endregion

            #region 恶龙属性
            int dragonX = 30;
            int dragonY = 20;
            int dragonAtkMin = 8;
            int dragonAtkMax = 13;
            int dragonHp = 100;
            #endregion

            #region 公主属性
            int princessX = 30;
            int princessY = 10;
            #endregion

            int fightTurn = 0;

            while (true)
            {
                if (dragonHp > 0)
                {
                    Console.SetCursorPosition(dragonX, dragonY);
                    Console.ForegroundColor = ConsoleColor.Green;
                    Console.Write('▲');
                }
                else
                {
                    Console.SetCursorPosition(dragonX, dragonY);
                    Console.Write("  ");
                    Console.SetCursorPosition(princessX, princessY);
                    Console.ForegroundColor = ConsoleColor.Blue;
                    Console.Write('◎');
                }

                Console.SetCursorPosition(playerX, playerY);
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.Write('★');

                if(isOver)
                {
                    Console.ReadKey(true);
                    sceneId++;
                    endMessage = "迎娶公主";
                    break;
                }
                
                if(playerHp <= 0)
                {
                    Console.ReadKey(true);
                    endMessage = "无名之碑";
                    sceneId++;
                    break;
                }

                getKey = Console.ReadKey(true).KeyChar;

                Console.SetCursorPosition(playerX, playerY);
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.Write("  ");

                switch (getKey) 
                {
                    case 'W':
                    case 'w':
                        if (isFight) continue;
                        playerDx = 0;
                        playerDy = -1;
                        if (playerX + playerDx == dragonX && playerY + playerDy == dragonY && dragonHp > 0) continue;
                        if (playerX + playerDx == princessX && playerY + playerDy == princessY && dragonHp <= 0) continue;
                        if (playerY >= 2) --playerY;
                        break;

                    case 'A':
                    case 'a':
                        if (isFight) continue;
                        playerDx = -2;
                        playerDy = 0;
                        if (playerX + playerDx == dragonX && playerY + playerDy == dragonY && dragonHp > 0) continue;
                        if (playerX + playerDx == princessX && playerY + playerDy == princessY && dragonHp <= 0) continue;
                        if (playerX >= 4) playerX -= 2;
                        break;
                    case 'S':
                    case 's':
                        if (isFight) continue;
                        playerDx = 0;
                        playerDy = 1;
                        if (playerX + playerDx == dragonX && playerY + playerDy == dragonY && dragonHp > 0) continue;
                        if (playerX + playerDx == princessX && playerY + playerDy == princessY && dragonHp <= 0) continue;
                        if (playerY + 1 < h - 7) ++playerY;
                        break;
                    case 'D':
                    case 'd':
                        if (isFight) continue;
                        playerDx = 2;
                        playerDy = 0;
                        if (playerX + playerDx == dragonX && playerY + playerDy == dragonY && dragonHp > 0) continue;
                        if (playerX + playerDx == princessX && playerY + playerDy == princessY && dragonHp <= 0) continue;
                        if (playerX + 2 < w - 2) playerX += 2;
                        break;
                    case 'j':
                    case 'J':
                        //清空消息栏
                        for (int i = h - 6; i < h - 1; i++)
                        {
                            Console.SetCursorPosition(2, i);
                            Console.Write("                                            ");
                        }
                        if (playerX + playerDx == dragonX && playerY + playerDy == dragonY && dragonHp > 0)
                        {
                            isFight = true;
                            if(fightTurn == 0)
                            {
                                int nowAtk = random.Next(playerAtkMin, playerAtkMax + 1);
                                dragonHp = Math.Max(0, dragonHp - nowAtk);
                                Console.SetCursorPosition(2, h - 5);
                                Console.Write("勇者对恶龙造成{0}点伤害", nowAtk);
                                if (dragonHp <= 0)
                                {
                                    isFight = false;
                                    Console.SetCursorPosition(2, h - 4);
                                    Console.Write("你杀死了恶龙！");
                                }
                            }
                            else
                            {
                                int nowAtk = random.Next(dragonAtkMin, dragonAtkMax + 1);
                                playerHp = Math.Max(0, playerHp - nowAtk);
                                Console.SetCursorPosition(2, h - 5);
                                Console.Write("恶龙对勇者造成{0}点伤害", nowAtk);
                                if (playerHp <= 0)
                                {
                                    isFight = false;
                                    Console.SetCursorPosition(2, h - 4);
                                    Console.Write("你死了！");
                                }
                            }
                            fightTurn = (fightTurn + 1) % 2;
                            Console.SetCursorPosition(2, h - 6);
                            Console.Write("勇者hp:{0}     恶龙hp:{1}", playerHp, dragonHp);

                        }
                        //触发公主剧情
                        else if(playerX + playerDx == princessX && playerY + playerDy == princessY && dragonHp <= 0)
                        {
                            Console.SetCursorPosition(2, h - 6);
                            Console.Write("谢谢你救我，勇者！");
                            Console.SetCursorPosition(2, h - 5);
                            Console.Write("我愿意嫁给你！");
                            isOver = true;
                        }
                        
                        break;
                }
            }
            break;

        case 2:
            Console.Clear();
            Console.SetCursorPosition(w / 2 - 4, 6);
            Console.ForegroundColor = ConsoleColor.White;
            Console.Write("游戏结束");
            Console.SetCursorPosition(w / 2 - 8, 8);
            Console.ForegroundColor = ConsoleColor.White;
            Console.Write("获得称号:{0}",endMessage);
            Console.SetCursorPosition(w / 2 - 4, 10);
            Console.ForegroundColor = selectId0 == 0 ? ConsoleColor.Red : ConsoleColor.White;
            Console.Write("返回标题");
            Console.SetCursorPosition(w / 2 - 4, 14);
            Console.ForegroundColor = selectId0 == 1 ? ConsoleColor.Red : ConsoleColor.White;
            Console.Write("退出游戏");
            getKey = Console.ReadKey(true).KeyChar;
            if (getKey == 'w' || getKey == 'W')
            {
                selectId0 = (selectId0 - 1 + selectId0Num) % selectId0Num;
            }
            else if (getKey == 'S' || getKey == 's')
            {
                selectId0 = (selectId0 + 1) % selectId0Num;
            }
            else if (getKey == 'j' || getKey == 'J')
            {
                if (selectId0 == 0) sceneId = 0;
                else Environment.Exit(0);
            }
            break;
    }
}
```