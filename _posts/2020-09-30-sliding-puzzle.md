---
layout: post
title: DFS_BFS之滑动谜题[Shiba Inu]
categories: BFS_DFS
description: DFS_BFS之滑动谜题[Shiba Inu]
keywords: DFS, BFS
---

## DFS_BFS之滑动谜题[Shiba Inu]

![shiba-inu-1770788_640](/images/posts/algorithm/dfs_bfs/un-classify/shiba-inu-1770788_640.png)



![image-20200930083020679](/images/posts/algorithm/dfs_bfs/un-classify/image-20200930083020679.png)

### 方法1:BFS

![image-20200930082830170](/images/posts/algorithm/dfs_bfs/un-classify/image-20200930082830170.png)

> 上图解释了dirs数组的由来

关联阅读：[二维矩阵的常见转换技巧](https://wat1r.github.io/2020/09/29/two-direction-array-skill/)

```java
    {% raw %}
	int[][] dirs = {{1, 3}, {0, 2, 4}, {1, 5}, {0, 4}, {1, 3, 5}, {2, 4}};
	{% endraw %}

    public int slidingPuzzle(int[][] board) {
        String start = "";
        int m = board.length, n = board[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                start += board[i][j];
            }
        }
        String end = "123450";
        Queue<String> queue = new LinkedList<>();
        queue.offer(start);
        Set<String> visited = new HashSet<>();
        visited.add(start);
        int level = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int k = 0; k < size; k++) {
                //找到目标位置，退出
                String curr = queue.poll();
                if (curr.equals(end)) {
                    return level;
                }
                //找到0对应想idx
                int zeroIdx = curr.indexOf("0");
                for (int d : dirs[zeroIdx]) {
                    //swap 判断next
                    String next = swap(curr, zeroIdx, d);
//                    System.out.printf("curr:%s-->next:%s\n", curr, next);
                    if (!visited.contains(next)) {
                        queue.offer(next);
                        visited.add(next);
                    }
                }
            }
//            PrintUtils.printMatrix(board);
            level++;
        }
        return -1;
    }

    /**
     * 交换一个 str的i与j未知的字符，生成一个新的字符返回
     * @param str
     * @param i
     * @param j
     * @return
     */
    private String swap(String str, int i, int j) {
        StringBuilder sb = new StringBuilder(str);
        sb.setCharAt(i, str.charAt(j));
        sb.setCharAt(j, str.charAt(i));
        return sb.toString();
    }
```



### Reference

- https://leetcode.com/problems/sliding-puzzle/discuss/146652/Java-8ms-BFS-with-algorithm-explained