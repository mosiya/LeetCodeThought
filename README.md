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
+ 2020.07.30 914. 卡牌分组 and 66. 加一 and 661. 图片平滑器 and 219. 存在重复元素 II and 1304. 和为零的N个唯一整数 and 169. 多数元素 and 1. 两数之和 and 1385. 两个数组间的距离值
+ 2020.08.03 1128. 等价多米诺骨牌对的数量
+ 2020.08.04 766. 托普利茨矩阵 and 1185. 一周中的第几天 and 867. 转置矩阵
+ 2020.08.05 448. 找到所有数组中消失的数字 and 1295. 统计位数为偶数的数字 and 747. 至少是其他数字两倍的最大数 and 561. 数组拆分 I
+ 2020.08.06 119. 杨辉三角 II and 剑指 Offer 53 - I. 在排序数组中查找数字 I and 1018. 可被 5 整除的二进制前缀 and 1450. 在既定时间做作业的学生人数 and 1343. 大小为 K 且平均值大于等于阈值的子数组数目 and 面试题 16.04. 井字游戏
+ 2020.08.07 剑指 Offer 29. 顺时针打印矩阵 and 1431. 拥有最多糖果的孩子 and 566. 重塑矩阵 and 628. 三个数的最大乘积 and 717. 1比特与2比特字符
+ 2020.08.10 1470. 重新排列数组 and 面试题 01.01. 判定字符是否唯一 and 746. 使用最小花费爬楼梯
+ 2020.08.11 1365. 有多少小于当前数字的数字 and 1337. 方阵中战斗力最弱的 K 行 and 面试题 16.17. 连续数列 and 1480. 一维数组的动态和 and 509. 斐波那契数
+ 2020.08.12 1534. 统计好三元组 and 1260. 二维网格迁移
+ 2020.08.13 849. 到最近的人的最大距离 and 724. 寻找数组的中心索引 and 905. 按奇偶排序数组 and 1200. 最小绝对差
+ 2020.08.14 1013. 将数组分成和相等的三个部分 and 1464. 数组中两元素的最大乘积 and 414. 第三大的数 and 1399. 统计最大组的数目 and 1331. 数组序号转换 and 剑指 Offer 04. 二维数组中的查找


#### 关于数组的算法，可以使用的小技巧：

+ 使用后就删除
+ 求多个最大或者最小元素：628. 三个数的最大乘积

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
+ 使用正负号标记元素
+ 使用二进制高位存储：1470. 重新排列数组

求k个元素和
+ 滑动窗口
+ 累加数组
+ 累加数组相减
+ 每次累加重置max

求元素频次超过半数：面试题 17.10. 主要元素、169. 多数元素
+ 摩尔投票法
+ 二进制数值判断
+ 若不超过半数则需要验证

棋盘类题目
+ 方向数组：999. 可以被一步捕获的棋子数、661. 图片平滑器

求两数最大公约数
+ 辗转相除法(欧几里得算法)：914. 卡牌分组