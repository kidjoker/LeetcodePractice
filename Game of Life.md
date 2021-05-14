# Game of Life
#每日技术

### 题目
According to  [Wikipedia's article](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life) : "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."
The board is made up of an m x n grid of cells, where each cell has an initial state: live (represented by a 1) or dead (represented by a 0). Each cell interacts with its  [eight neighbors](https://en.wikipedia.org/wiki/Moore_neighborhood)  (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):
	1	Any live cell with fewer than two live neighbors dies as if caused by under-population.
	2	Any live cell with two or three live neighbors lives on to the next generation.
	3	Any live cell with more than three live neighbors dies, as if by over-population.
	4	Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction

### 解题思路
题目里说了不能改变当前数组的数据，但是0和1只能存储两种信息（生或死），所以我们通过两次遍历，现将变化的数据记录下来（死->生为2 生->死为3），然后再遍历的时候把数据修改回去

因为修改原数据不能改变结果，所以在统计周围的活细胞数量的时候，就需要考虑3的情况

### 代码
```java
	public void gameOfLife(int[][] board) {
        int height = board.length;
        int width = board[0].length;
        
        for(int i = 0; i < height; i++){
            for(int j = 0; j < width; j++){
                if(board[i][j] == 0){
                    if(count(board,i,j) == 3){
                        board[i][j] = 2;
                    }
                }
                
                if(board[i][j] == 1){
                    if(count(board,i,j) < 2 || count(board,i,j) > 3){
                        board[i][j] = 3;
                    }
                }
            }
        }
        
        for(int i = 0; i < height; i++){
            for(int j = 0; j < width; j++){
                if(board[i][j] == 2){
                    board[i][j] = 1;
                }
                
                if(board[i][j] == 3){
                    board[i][j] = 0;
                }
            }
        }
    }
    
    private int count(int[][] board, int i, int j){
        int[][] directions = {{-1,0},{0,1},{1,0},{0,-1},{-1,-1},{1,1},{-1,1},{1,-1}};
        int res = 0;
        
        int height = board.length;
        int width = board[0].length;
        for(int[] dir : directions){
            if(i+dir[0] >= 0 && i+dir[0] < height && j+dir[1] >= 0 && j+dir[1] < width){
                if(board[i+dir[0]][j+dir[1]] == 1 || board[i+dir[0]][j+dir[1]] == 3){
                    res++;
                }
            }
        }
        
        return res;
    }
```

### 参考资料
https://youtu.be/9AsUixzUGa0