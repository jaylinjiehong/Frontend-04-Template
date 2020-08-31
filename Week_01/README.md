## 第一周学习总结
### 1、知识体系脑图
#### 追溯法
-   源头：

    -   最早出现的论文、杂志；最初的实际案例

-   标准和文档：
    -   W3.org
    -   developer.mozilla.org
    -   msdn.microsoft.com
    -   developer.apple.com

-   大师
    -   Tim Berners-Lee
    -   Brendan Eich
    -   Bjarne Stroustrup

#### 个人短板
-   由于自身日常工作主要是从事客户端Android开发，对于前端知识体系缺乏总结整理，看到winter老师总结的知识体系，感觉如果使用追溯法进行追踪，耗费时间真的有点久，有点不知所措。后续需要在实践过程中，不断积累。

### 2、前端目录
-   个人对于前端开发目录整理，偏向于从前端要解决的问题入手，从前端是如何从底层语言诞生来，是为了解决什么问题，然后是如何发展壮大。毕竟，前端是跑在操作系统管理的进程之中。javaScript是c++依靠编译原理的理论，创造的虚拟机来跑的语言，如果能理解到javaScript代码执行过程时，最终机器语言的运转过程，那对于前端能有不一样的思考。

### 3、TicTacToe练习

-   对于AI功能的代码，刚开始自己有点人肉递归地理解，感觉晕圈

```
 function bestChoice(pattern,color){
        let point = willWin(pattern,color);
        if(point){
            return{
                point:point,
                result:1
            }
        }
        let result = -1;
        outer:for(let i=0;i<3;i++){
            for(let j =0;j<3;j++){
                if(pattern[i*3+j]!==0){
                    continue;
                }
                let tmp = clone(pattern);
                tmp[i*3+j] = color;
                let oop = bestChoice(tmp,3-color);

               //对方的最差是我方的最好 
                if(-oop.result >= result){
                    result = -oop.result;
                    point = [j,i];
                }
                if(result==1){
                    break outer;
                }
            }
        }
        return{
            point:point,
            result:point?result:0
        }
    }
```
-   后来，想着如果采用递归的模板和剪枝的思想来理解。
-   思维重点
    -   1、不要人肉进行递归（最大误区）
    -   2、找到最近最简方法，将其拆解成可重复解决的问题（重复子问题）
    -   3、数学归纳法思维

```
 function bestChoice(pattern,color){
     <!-- 1、terminator（递归终止条件） -->
        let point = willWin(pattern,color);
        if(point){
            return{
                point:point,
                result:1
            }
        }
        <!-- 2、process current logic（处理本层逻辑） -->
        let result = -1;
        outer:for(let i=0;i<3;i++){
            for(let j =0;j<3;j++){
                if(pattern[i*3+j]!==0){
                    continue;
                }
                let tmp = clone(pattern);
                tmp[i*3+j] = color;
                <!-- 3、drill down （下探到下一层） -->
                let oop = bestChoice(tmp,3-color);

               //对方的最差是我方的最好 
                if(-oop.result >= result){
                    result = -oop.result;
                    point = [j,i];
                }
                if(result==1){
                    break outer;
                }
            }
        }

        <!-- 4 restore current status（保存本层状态） -->
        return{
            point:point,
            result:point?result:0
        }  
    }
```

-   果然，需求就是：
    -   假设我方下一步是第n步，对方的下一步是第n+1步。
    -   递归的终止条件：我方赢了，就终止。
    -   我方的best(n)的最好结果是对方best(n+1)的最差结果。是best(n)=-best(n+1)。
    -   剪枝的实现就是当我方出现赢的情况了，就不递归了，减去剩下的递归分支。
    -   类似dfs的遍历过程，对于满足条件之后，就剪去剩下遍历过程。

#### AI总结
-   对于算法理解还有待提升，递归+dfs+剪枝，与实际问题的结合。

### 五子棋游戏
-   [五子棋](https://zh.wikipedia.org/wiki/%E4%BA%94%E5%AD%90%E6%A3%8B)
-   [五子棋 （两人对弈的策略型棋类游戏）](https://baike.baidu.com/item/%E4%BA%94%E5%AD%90%E6%A3%8B/130266)

### 追溯法：面向对象概念
-   [object-oriented programming (OOP)](https://searchapparchitecture.techtarget.com/definition/object-oriented-programming-OOP)
-   [OOP Javascript Vs Java(or others, such as PHP)](https://stackoverflow.com/questions/8025093/oop-javascript-vs-javaor-others-such-as-php)
