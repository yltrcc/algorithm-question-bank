# 题目链接

[http://poj.org/problem?id=1116](http://poj.org/problem?id=1116)

# Description

Castaway Robinson Crusoe is living alone on a remote island. One day a ship carrying a royal library has wrecked nearby. Usually Robinson brings any useful stuff from the shipwreck to his island, and this time he has brought a big chest with books.

Robinson has decided to build a bookcase for these books to create his own library. He cut a rectangular niche in the rock for that purpose, hammered in wooden pegs, and placed wooden planks on every pair of pegs that have the same height, so that all planks are situated horizontally and suit to act as shelves.

Unfortunately, Robinson has discovered that one especially old and big tome does not fit in his bookcase. He measured the height and width of this tome and has decided to redesign his bookcase in such a way, as to completely fit the tome on one of the shelves, taking into account locations of other shelves and the dimensions of the niche. With each shelf in the bookcase, one of the following operations should be made:

鲁滨逊决定做一个书架，建立自己的藏书室。他在石头墙上凿了一个矩形壁龛， 把一些栓子钉入墙体，然后找来一些木板架在两个水平的栓子上做成书架，任意两块木板不处在同一水平线上，如图1-2所示。不巧的是，鲁滨逊忽然发现有一本珍贵的旧书特别大，无法放进他现在架好的书架里。他仔细量了这本大部头的高和厚，想改造一下他的书架，以便于把这本书放进去（别忘了，书架是做在墙里面的，不能超出范围）。

![](https://secure1.wostatic.cn/static/ibv4dcPX46aiaUzHj6vZrN/image.png)

1. Leave the shelf on its original place.
2. Move the shelf to the left or to the right.
3. Shorten the shelf by cutting off a part of the plank and optionally move it to the left or to the right.
4. Move one of the pegs to a different place at the same height and move the shelf to the left or to the right.
5. Shorten the shelf by cutting off a part of the plank, move one of the pegs to a different place at the same height, and optionally move the shortened shelf to the left or to the right.
6. Remove the shelf from the bookcase along with both supporting pegs.

We say that the shelf is properly supported by its pegs, if exactly two distinct pegs support the shelf and the center of the shelf is between its pegs or coincides with one of the pegs. The original design of Robinson's library has all the shelves properly supported by their pegs and lengths of all shelves are integer number of inches. The Robinson may only cut an integer number of inches from the planks, because he has no tools for more precise measurements. All remaining shelves after the redesign must be properly supported by their pegs.

You are to find the way to redesign Robinson's library to fit the special old tome without changing original design too much. You have to minimize the number of pegs that are to be removed from their original places during the redesign (operations 4 and 5 remove one peg, and operation 6 removes two pegs). If there are different ways to solve the problem, then you are to find the one that minimizes the total length of planks that are to be cut off (operations 3 and 5 involve cutting something from the planks, and operation 6 counts as if cutting off the whole plank). Width of planks and diameter of pegs shall be considered zero.

The tome may not be rotated. The tome should completely (to all its width) stand on one of the shelves and may only touch other shelves, their pegs or niche's edge.



下面是一些改造的操作方法：

1. 把架子留在原地不动；
2. 把木板向左移或者向右移
3. 把木板锯掉一段向左或向右移；
4. 把栓子移到与原来位置处于同一水平线的另一个位置，并把木板左移或者右移；
5. 把木板锯掉一段，移动某一栓子到同一水平线上另一个位置，并把木板左移或者右移；
6. 把木板和两个栓子一起拿掉。

当木板被两个栓子架住，并且木板的中心在两个栓子之间或恰在一个栓子上方时，这个书架是稳定的。鲁滨逊开始设计的藏书室里所有的书架都是稳定的。木板的长度是整数，单位是英寸。因为测量工具不够精确，他只能做到以英寸为单位切割木板。在你的改造中，所有的书架必须始终是稳定的。

要找到一个方案来改造鲁滨逊的藏书室，以便于那本古老的大书放进去，而且要使改动尽量少。要尽量减少移动的栓子数目（操作4、5每次移动一个栓子，操作6每次移动两个），在这个前提下，找到浪费木板长度最小的方案（操作3、5各切割掉一定长度，操作6把整个木板的长度都浪费了）。木板的厚度和栓子直径忽略不计。那本大书只能竖直放置，它的全部厚度都要位于木板上，而且只可以碰到其他木板或栓子的边缘。



# Input

The first line of the input file contains four integer numbers XN, YN, XT, and YT, separated by spaces. They are, correspondingly, width and height of the niche, and width and height of the old tome in inches (1 <= XN, YN, XT, YT <= 1000).

The second line of the input file contains a single integer number N (1 <= N <= 100) that represents the number of the shelves. Then N lines follow. Each line represents a single shelf along with its two supporting pegs, and contains five integer numbers yi, xi, li, x1i, x2i, separated by spaces, where:

?yi (0 < yi < YN) - the height of the ith shelf above the bottom of the niche in inches.

?xi (0 <= xi < XN) - the distance between the left end of the ith shelf and the left edge of the niche in inches.

?li (0 < li <= XN - xi) - the length of the ith shelf in inches.

?x1i (0 <= x1i <= li/2) - the distance between the left end of the ith shelf and its leftmost supporting peg in inches.

?x2i (li/2 <= x2i <= li; x1i < x2i) - the distance between the left end of the ith shelf and its rightmost supporting peg in inches.

All shelves are situated on different heights and are properly supported by their pegs. The problem is guaranteed to have a solution for the input data.

# Output

The output file shall contain two integer numbers separated by a space. The first one is the minimal number of pegs that are to be removed by Robinson from their original locations to place the tome. The second one is the minimal total length of planks in inches that are to be cut off during the redesign that removes the least number of pegs.

# Sample Input

```text
11 8 4 6
4
1 1 7 1 4
4 3 7 1 6
7 2 6 3 4
2 0 3 0 3
```

# Sample Output

```text
1 3
```



# 分析

题目中有一个条件：任意两块木板不处在同一水平线上。这样，某块木板移动后不会存在架在其他木板或木栓上的情况，因此我们可以孤立地考虑每块木板的移动与锯下，使问题复杂度大大降低。于是，我们很快指定了解题方案：

逐个枚举安放大书的位置然后选取其中最优的。



工作分两步：

1. 确立安放大书的位置
2. 用最优代价为大书腾出空间。

由于评价函数要求在移动最少木栓的前提下浪费最短的模板，而两个步骤又是独立 的，所以无论步骤1还是步骤2，都：

- 尝试“不移动木栓也不据木板”的方案，如果失败
- 尝试“不移动木栓但锯下最少木板”的方案，如果失败
- 尝试“移动一个木栓但不锯下木板”的方案，如果失败
- 尝试“移动一个木栓同时锯下最少木板”的方案，如果失败
- 尝试“撤去整个木板”的方案。



# 参考代码

```C++
#include<iostream>
#include<cstdio>
#include<algorithm>
using namespace std;
int xn,yyn,xt,yt,n,mindz=0x3f3f3f3f,minmb=0x3f3f3f3f;
struct node
{
    int x,y,l,x1,x2;
    friend bool operator <(node a,node b)
    {
        return a.y<b.y;//重载小于号，用来排序
    }
} p[105];
void move(int k,int x,int &dz,int &mb)
{
    for(int i=k+1; i<=n; i++) //木板是有序的，故在枚举完在第k个木板上放书后，要判断k以上的木板是否会阻挡书的放置
    {
        if(p[i].y>=p[k].y+yt)break;//以上的都挨不到书了；
        if(p[i].x+p[i].l<=x||p[i].x>x+xt)continue;//此木板不会对书架造成影响；
        if(p[i].x2<=x) //此木板右钉子在起始点左端；
        {
            int lst;//注意，可以通过左移来避免对书架造成影响
            if(x<=2*p[i].x1)//要考虑重心的问题
                lst=2*(x-p[i].x1);
            else
                lst=x;
            if(lst<p[i].l)mb+=p[i].l-lst;
        }
        else if(p[i].x1>=x+xt) //木板左钉子在终点的右端
        {
            int lst;//与上种情况同理
            if(p[i].x2-x-xt<=xn-p[i].x2)
                lst=2*(p[i].x2-x-xt);
            else lst=xn-x-xt;
            if(lst<p[i].l)mb+=p[i].l-lst;
        }
        else if(p[i].x1<=x&&p[i].x2>x&&p[i].x2<x+xt) //起始点钉子在钉子之间且终点在右钉子右边
        {
            if(x==0) //若起始点为零，只能删掉一整条边
            {
                dz+=2;
                mb+=p[i].l;
            }
            else //移钉
            {
                //注意：对于此情况，是将木板靠到最左边，最右的部分截掉；
                dz++;
                if(p[i].l>x)mb+=p[i].l-x;//截木板；
            }
        }
        else if(p[i].x1>x&&p[i].x1<x+xt&&p[i].x2>=x+xt) //左钉子在起始点与终点之间并且右钉子在终点的右端
        {
            if(x+xt==xn) //若终点到最右端了，只能删掉一整条边
            {
                dz+=2;
                mb+=p[i].l;
            }
            else //移钉
            {
                //注意：对于此情况，是将木板靠到最右边，最左的部分截掉；
                dz++;
                if(p[i].l>xn-x-xt)mb+=p[i].l-xn+x+xt;//截木板；
            }
        }
        else if(p[i].x1<=x&&p[i].x2>=x+xt) //两钉子在起点终点的两端之外
        {
            if(x==0&&xt==xn)//只能全拆掉
                dz+=2;
            else
                dz++;
            int lst=max(x,xn-x-xt);
            if(p[i].l>lst)
                mb+=p[i].l-lst;
        }
        else if(p[i].x1>x&&p[i].x2<x+xt) //不多想直接拆
        {
            dz+=2;
            mb+=p[i].l;
        }
    }
}
void solve(int k)
{
    for(int i=0; i<=xn-xt; i++) //枚举书的起始位置
    {
        int dz=0,mb=0;
        if(i+p[k].l<p[k].x1)continue;// 木板根本放不到钉子上，continue；
        if(2*(p[k].x1-i)>p[k].l||//重心出界（左钉子）
                2*(i+xt-p[k].x2)>p[k].l||//重心出界（右钉子）
                p[k].x2-i>p[k].l||//木板长度不够 （左端点到右钉子距离超过了木板长度）
                i+xt-p[k].x1>p[k].l)//木板长度不够 （右端点到左钉子距离超过了木板长度）
            dz++;//需要移动钉子，操作++；
        move(k,i,dz,mb);
        if(dz<mindz||(dz==mindz&&mb<minmb))
        {
            mindz=dz;
            minmb=mb;
        }
    }
}
int main()
{
    scanf("%d%d%d%d",&xn,&yyn,&xt,&yt);
    scanf("%d",&n);
    for(int i=1; i<=n; i++)
    {
        scanf("%d%d%d%d%d",&p[i].y,&p[i].x,&p[i].l,&p[i].x1,&p[i].x2);
        p[i].x1+=p[i].x;
        p[i].x2+=p[i].x;
    }
    sort(p+1,p+n+1);//按照书架的高度从低到高排序
    for(int i=1; i<=n; i++)
    {
        if(p[i].y+yt>yyn)break;//若从第i个书架的高度加上书的高度大于最大高度，书无法放在i以后的任何一个书架上，直接break；
        if(p[i].l>=xt)//若第i个书架可以放得下最大的那本书，则开始找其最小耗费
            solve(i);
    }
    printf("%d %d",mindz,minmb);
    return 0;
}

```