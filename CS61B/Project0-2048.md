cs61B 的第一个项目就是实现 2048 这个小游戏。如果思路清晰，写起来会比较轻松，大致用时1.5 - 2小时。

$\color{red}{笔者源代码在文末}$
### emptySpaceExists
描述:
```java
/** Returns true if at least one space on the Board is empty.  
 *  Empty spaces are stored as null. **/
public static boolean emptySpaceExists(Board b) {  
    // TODO: Fill in this function.  
    return false; 
}
```
可知，需要遍历板子，判断是否存在一个格子为空，如果找到一个，返回 return true，如果搜完未找到，则 return false;
如何获取板子的长度和宽度？
观察 Board 类，我们发现函数：
```java
/** Returns the size of the board. */  
public int size() {  
    return values.length;  
}
```
所以，调用 b.size() 即可获得板子的长度。
由此，我们可以写出大体框架。
```java
public static boolean emptySpaceExists(Board b) {  
    // TODO: Fill in this function.  
    for(int row = 0; row < b.size(); row ++)  {        
	    for(int col = 0; col < b.size(); col ++)  {            
		    if(...)  
                return true;  
        }    
    }        
    return false;  
}
```
可见，if 判断框里面的条件就是 格子为空。观察 Board 类和 Tile 类
b.tile(col, row) 返回 Null 如果这个格子为空
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240324134631.png)
因此，最终的代码为：
```java
public static boolean emptySpaceExists(Board b) {  
    // TODO: Fill in this function.  
    for(int row = 0; row < b.size(); row ++)  {        
	    for(int col = 0; col < b.size(); col ++)  {            
		    if(b.tile(col, row) == null)  
                return true;  
        }    
    }        
    return false;  
}
```


### maxTileExists
```java
/**  
 * Returns true if any tile is equal to the maximum valid value. * Maximum valid value is given by MAX_PIECE. Note that * given a Tile object t, we get its value with t.value(). */
 public static boolean maxTileExists(Board b) {  
    // TODO: Fill in this function.  
    return false;  
}
```
与 emptySpaceExists 类似，但是需要获取格子上的值。
在 Tile 类中。我们找到方法 value()
```java
/** Return the value supplied to my constructor. */  
public int value() {  
    return value;  
}
```
所以能写出
```java
public static boolean maxTileExists(Board b) {  
    // TODO: Fill in this function.  
    for(int col = 0; col < b.size(); col ++)  {        
	    for(int row = 0; row < b.size(); row ++)  {            
		    if(b.tile(col, row).value() == MAX_PIECE)  
	            return true;  
	    }
	}    
    return false;  
}
```
然而，测试出错。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240324135352.png)
因为没有考虑到空格子的问题。
所以我们加上
```java
if(b.tile(col, row) == null)  
    continue;
```
最终的代码为：
```java
public static boolean maxTileExists(Board b) {  
    // TODO: Fill in this function.  
    for(int col = 0; col < b.size(); col ++) {  
        for(int row = 0; row < b.size(); row ++) {  
            if(b.tile(col, row) == null)  
                continue;  
            if(b.tile(col, row).value() == MAX_PIECE)  
                return true;  
        }    
    }    
    return false;  
}
```


### atLeastOneMoveExists
```java
/**  
 * Returns true if there are any valid moves on the board. * There are two ways that there can be valid moves: * 1. There is at least one empty space on the board. * 2. There are two adjacent tiles with the same value. */
 public static boolean atLeastOneMoveExists(Board b) {  
    // TODO: Fill in this function.  
    return false;  
}
```
返回 true 的情况之一：
1. 至少存在一个空格子
2. 至少有两个相邻格子的值相同
其中条件一也就是 emptySpaceExists 返回 true
```java
 public static boolean atLeastOneMoveExists(Board b) {  
    // TODO: Fill in this function. 
    if(emptySpaceExists(b))  
	    return true; 
	
    return false;  
}
```
而是否存在两个相邻格子值相同。我们先遍历行列，取当前位置的格子，值记为 value_cur
从这个格子出发，遍历上下左右相邻格子。我们可以创建偏移数组，方便遍历
```java
int[] dx = {-1, 0, 1, 0};  
int[] dy = {0, 1, 0, -1};
```
当然，还要判断新位置有无下标越界
```java
public static boolean atLeastOneMoveExists(Board b) {  
    // TODO: Fill in this function.  
    if(emptySpaceExists(b))  
        return true;  
    boolean two = false;  
    int[] dx = {-1, 0, 1, 0};  
    int[] dy = {0, 1, 0, -1};  
    int size = b.size();  
    for(int col = 0; col < size; col ++) {  
        for(int row = 0; row < size; row ++){  
            int value_cur = b.tile(col, row).value();  
            for(int k = 0; k < 4; k ++){  
                int cur_col = col + dy[k];  
                int cur_row = row + dx[k];  
                if(cur_col > 0 && cur_col < size && cur_row > 0 && cur_row < size && b.tile(cur_col, cur_row).value() == value_cur)  
                    return true;  
            }        
        }    
    }    
    return false;  
}
```


## Building the Game Logic
### tilt
```java
public boolean tilt(Side side) {  
    boolean changed;  
    changed = false;  
  
    // TODO: Modify this.board (and perhaps this.score) to account  
    // for the tilt to the Side SIDE. If the board changed, set the  
    // changed local variable to true.  
    checkGameOver();  
    if (changed) {  
        setChanged();  
    }    
    return changed;  
}
```
先只考虑方向向上：
	我们可以考虑先将整个棋盘往上移动，让所有格子向上，填补掉格子上方的空格子，先不做合并处理。
	需要注意的一点是，棋盘左下角是(0, 0)。
	以列为基础。我们先从倒数第二行，从最上面一行的下面一行开始，向上搜寻有多少个空格子。然后再进行向上移动。同时，进行了移动需要将 changed 设置为 true
```java
// 对于每一列，先找到能向上移动的最大位置（找空格数）  
for(int col = 0; col < size; col ++) {  
    for (int row = size - 2; row >= 0; row--) {  
        int nulltile = 0;  
        Tile t = board.tile(col, row);  
        if(t != null) {  
            for(int row_before = row + 1; row_before < size; row_before ++){  
                if(tile(col, row_before) == null)  
                    nulltile ++;  
            }            
	        board.move(col, row + nulltile, t);  
            changed = true;  
        }    
    }
}
```
之后，我们对相同的格子进行合并，只考虑方向向上，那么就是 该位置的格子如果和它上一个格子的值相同，那么该格子向上移动，同时分数增加该格子值的两倍。
```java
for(int col = 0; col < size; col ++){  
    for(int row = size - 2; row >= 0; row --){  
        Tile t1 = board.tile(col, row);  
        if(t1 != null){  
            Tile t2 = board.tile(col, row + 1);  
            if(t2 != null && t1.value() == t2.value()){  
                board.move(col, row + 1, t1);  
                changed = true;  
                score += 2 * t2.value();  
            }        
        }    
    }
}
```
到这里还没有结束，因为如果向上移动了，那么该格子又变成了空格子，所以我们又要重复之前的处理空格子的操作，整体向上移动。
结果如下：
```java
public boolean tilt(Side side) {  
    boolean changed;  
    changed = false;  
  
    // TODO: Modify this.board (and perhaps this.score) to account  
  
    int size = board.size();  
  
    // 对于每一列，先找到能向上移动的最大位置（找空格数）  
    for(int col = 0; col < size; col ++) {  
        for (int row = size - 2; row >= 0; row--) {  
            int nulltile = 0;  
            Tile t = board.tile(col, row);  
            if(t != null) {  
                for(int row_before = row + 1; row_before < size; row_before ++){  
                    if(tile(col, row_before) == null)  
                        nulltile ++;  
                }                
		        board.move(col, row + nulltile, t);  
                changed = true;  
            }        
        }    
    }  
    for(int col = 0; col < size; col ++){  
        for(int row = size - 2; row >= 0; row --){  
            Tile t1 = board.tile(col, row);  
            if(t1 != null){  
                Tile t2 = board.tile(col, row + 1);  
                if(t2 != null && t1.value() == t2.value()){  
                    board.move(col, row + 1, t1);  
                    changed = true;  
                    score += 2 * t2.value();  
                }            
            }        
        }    
    }  
    for(int col = 0; col < size; col ++) {  
        for (int row = size - 2; row >= 0; row--) {  
            int nulltile = 0;  
            Tile t = board.tile(col, row);  
            if(t != null) {  
                for(int row_before = row + 1; row_before < size; row_before ++){  
                    if(tile(col, row_before) == null)  
                        nulltile ++;  
                }                
	            board.move(col, row + nulltile, t);  
                changed = true;  
            }        
        }    
    }  

    // for the tilt to the Side SIDE. If the board changed, set the  
    // changed local variable to true.  
    checkGameOver();  
    if (changed) {  
        setChanged();  
    }    
    return changed;  
}
```
但是上述代码只针对了方向向上。
官方提供了函数 $setViewingPerspective$，

> For this problem, we’ve given away a clean solution. This will allow you to handle the other three directions with only two additional lines of code! Specifically, the `Board` class has a `setViewingPerspective(Side s)` function that will change the behavior of the `tile` and `move` classes so that they _behave as if the given side was NORTH_.

也就是我们现在操作前加上
```java
if(side != Side.NORTH)  
    board.setViewingPerspective(side);
```

当然，在最后还需要将视角恢复

> Important: Make sure to use `board.setViewingPerpsective` to set the perspective back to `Side.NORTH` before you finish your call to `tilt`, otherwise weird stuff will happen.

最后添加上
```java
if(side != Side.NORTH)  
    board.setViewingPerspective(Side.NORTH);
```

最终代码为：
```java
public boolean tilt(Side side) {  
    boolean changed;  
    changed = false;  
  
    // TODO: Modify this.board (and perhaps this.score) to account  
  
    int size = board.size();  

	if(side != Side.NORTH)  
	    board.setViewingPerspective(side);
  
    // 对于每一列，先找到能向上移动的最大位置（找空格数）  
    for(int col = 0; col < size; col ++) {  
        for (int row = size - 2; row >= 0; row--) {  
            int nulltile = 0;  
            Tile t = board.tile(col, row);  
            if(t != null) {  
                for(int row_before = row + 1; row_before < size; row_before ++){  
                    if(tile(col, row_before) == null)  
                        nulltile ++;  
                }                
		        board.move(col, row + nulltile, t);  
                changed = true;  
            }        
        }    
    }  
    for(int col = 0; col < size; col ++){  
        for(int row = size - 2; row >= 0; row --){  
            Tile t1 = board.tile(col, row);  
            if(t1 != null){  
                Tile t2 = board.tile(col, row + 1);  
                if(t2 != null && t1.value() == t2.value()){  
                    board.move(col, row + 1, t1);  
                    changed = true;  
                    score += 2 * t2.value();  
                }            
            }        
        }    
    }  
    for(int col = 0; col < size; col ++) {  
        for (int row = size - 2; row >= 0; row--) {  
            int nulltile = 0;  
            Tile t = board.tile(col, row);  
            if(t != null) {  
                for(int row_before = row + 1; row_before < size; row_before ++){  
                    if(tile(col, row_before) == null)  
                        nulltile ++;  
                }                
	            board.move(col, row + nulltile, t);  
                changed = true;  
            }        
        }    
    }  

	if(side != Side.NORTH)  
	    board.setViewingPerspective(Side.NORTH);

    // for the tilt to the Side SIDE. If the board changed, set the  
    // changed local variable to true.  
    checkGameOver();  
    if (changed) {  
        setChanged();  
    }    
    return changed;  
}
```
当然，两次填补空格子的操作是相同的。所以可以简化为一个函数。然后调用两次。
但是笔者不太会 java。
## Windows 可能运行时无法用方向键控制
进入 GUISource.java
将方向键替换为 W、D、S、A
如下
```java
switch (command) {  
    case "W" :  
        command = "Up";  
        break;  
    case "D" :  
        command = "Right";  
        break;  
    case "S" :  
        command = "Down";  
        break;  
    case "A" :  
        command = "Left";  
        break;  
    default :  
        break;  
}
```

到此，就完成了第一个 project（耗时近 2 小时）

### 笔者源代码
[点击此处](https://github.com/DaphneOdera17/cs61b-sp21/tree/main/proj0/game2048)
