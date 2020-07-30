## LeetCodeThought

懒得要命的自己，是时候改变了，坚持刷题，坚持改变自己吧

### 更新记录

#### Array

简单难度
+ 2020.07.13 1051. 高度检查器
+ 2020.07.14 剑指 Offer 53 - II. 0～n-1中缺失的数字 and 674. 最长连续递增序列 and 26. 删除排序数组中的重复项
+ 2020.07.21 88. 合并两个有序数组 and 1160. 拼写单词
+ 2020.07.22 1491. 去掉最低工资和最高工资后的工资平均值 and 118. 杨辉三角 and 35. 搜索插入位置 and 1299. 将每个元素替换为右侧最大元素
+ 2020.07.23 167. 两数之和 II - 输入有序数组 and 1266. 访问所有点的最小时间 and 1010. 总持续时间可被 60 整除的歌曲
+ 2020.07.24 1351. 统计有序矩阵中的负数
+ 2020.07.25 1089. 复写零
+ 2020.07.27 605. 种花问题 and 1346. 检查整数及其两倍数是否存在 and 643. 子数组最大平均数 I and 1122. 数组的相对排序
+ 2020.07.28 53. 最大子序和 and 1184. 公交站间的距离 and 697. 数组的度
+ 2020.07.29 面试题 17.10. 主要元素 and 1232. 缀点成线 and 999. 可以被一步捕获的棋子数
+ 2020.07.30 914. 卡牌分组 and 66. 加一



#### 关于数组的算法，可以使用的小技巧：

有序数组
+ 二分查找
+ 逆序遍历
+ 双指针遍历
+ 建立哈希表(元素唯一等情况)

无序数组
+ 排序
+ 建立哈希表(如统计元素出现次数、两数和以及其变种题)

有序二维数组：1351. 统计有序矩阵中的负数
+ 找到一个角，两个方向分别为非递增和非递减
+ 也可以选用二分查找

原地替换数组：1089. 复写零、88. 合并两个有序数组、1299. 将每个元素替换为右侧最大元素
+ 双指针（头尾指针、快慢指针）
+ 逆序遍历

求k个元素和
+ 滑动窗口
+ 累加数组
+ 累加数组相减
+ 每次累加重置max

求元素频次超过半数：面试题 17.10. 主要元素
+ 摩尔投票法
+ 二进制数值判断
+ 若不超过半数则需要验证

棋盘类题目
+ 方向数组：999. 可以被一步捕获的棋子数

求两数最大公约数
+ 辗转相除法(欧几里得算法)：914. 卡牌分组