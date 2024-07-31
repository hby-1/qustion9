# 可以形成最大正方形的矩形数目

给你一个数组 `rectangles` ，其中 `rectangles[i] = [li, wi]` 表示第 `i` 个矩形的长度为 `li` 、宽度为 `wi` 。

如果存在 `k` 同时满足 `k <= li` 和 `k <= wi` ，就可以将第 `i` 个矩形切成边长为 `k` 的正方形。例如，矩形 `[4,6]` 可以切成边长最大为 `4` 的正方形。

设 `maxLen` 为可以从矩形数组 `rectangles` 切分得到的 **最大正方形** 的边长。

请你统计有多少个矩形能够切出边长为 `maxLen` 的正方形，并返回**矩形** **数目** 。

## 示例 1：
>### 输入：
>rectangles = [[5,8],[3,9],[5,12],[16,5]]
>### 输出：
>3

## 示例 2：
>### 输入：
>rectangles = [[2,3],[3,7],[4,3],[3,7]]
>### 输出：
>3

## 代码：

1.(空间，时间复杂度较大)

    public class Solution {
        public int CountGoodRectangles(int[][] rectangles) {
            int[] minValue=new int[rectangles.Length];
            int count=0;
            for(int i=0;i<rectangles.Length;i++){
                minValue[i]=rectangles[i].Min();
            }
            for(int i=0;i<minValue.Length;i++){
                if(minValue[i]==minValue.Max()){
                    count++;
                }
            }
            return count;
        }
    }

2.

    public class Solution {
        public int CountGoodRectangles(int[][] rectangles) {
        int maxLen = 0;
            Dictionary<int, int> lengthCount = new Dictionary<int, int>();

            // 遍历矩形，计算每个矩形能切出的最大正方形边长
            foreach (var rectangle in rectangles)
            {
                int maxSquareLen = Math.Min(rectangle[0], rectangle[1]);

                if (maxSquareLen > maxLen)
                {
                    maxLen = maxSquareLen;
                }

                if (!lengthCount.ContainsKey(maxSquareLen))
                {
                    lengthCount[maxSquareLen] = 0;
                }
                lengthCount[maxSquareLen]++;
            }

            // 返回可以切出最大边长正方形的矩形数量
            return lengthCount[maxLen];
        }
    }

3.

    public class Solution {
        public int CountGoodRectangles(int[][] rectangles) {
            int maxLen = 0, count = 0;
            foreach (int[] rectangle in rectangles) {
                int sideLen = Math.Min(rectangle[0], rectangle[1]);
                if (sideLen == maxLen) {
                    count++;
                } else if (sideLen > maxLen) {
                    maxLen = sideLen;
                    count = 1;
                }
            }
            return count;
        }
    }

