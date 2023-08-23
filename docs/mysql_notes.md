# Mysql notes 
1. 语句执行顺序
   - 1-from
   - 2-join
   - 3-on
   - 4-where
   - 5-group by
   - 6-聚合函数
   - 7-having
   - 8-select
   - 9-distinct
   - 10-order by
   - 11-limit

2. 处理数值
   - 1. 整数与浮点数精度处理函数
      - TRUNCATE、ROUND、CEIL、FLOOR
   - 2. 字符串转化成数值
      - CAST、CONVERT
   - 3. 求余数函数-判断奇偶数
      - MOD、%

3. 字符串类型
   - 1. 取子串字符 left( ) 、right( ) 、substring( )
   - 2. 清洗空格 rtrim( ) 、ltrim( ) 、trim( )
   - 3. 替换 replace( )
   - 4. 字符串的拼接 concat( ) concat_ws( )

4. 日期
   - 1. 将字符串转变为日期
      - STR_TO_DATE(string, format_mask)
   - 2. 日期格式随心变
      - DATE_FORMAT(date, format)
   - 3. 提取日期片段（年、月、周、日）
      - year(current_date)
      - month(current_date)
      - week(current_date)
      - day(current_date)
   - 4. 时间平移大法
      - 本月的第一天
        - DATE_FORMAT(current_date, '%Y-%m-01')
      - 本月的最后一天
        - last_day(current_date)
      - 往前推两天
        - date_add(current_date, interval -2 day)
      - 往后推两天
        - date_add(current_date, interval +2 day)
      - 上个月的今天
        - date_add(current_date, interval -1 month)

5. 聚合取数
   - COUNT(col) - 返回所有非空值的个数
      - (区分 COUNT(*) 与 COUNT(字段)，后者空值不计入)
   - AVG(col) - 返回平均值
   - SUM(col) - 返回总和
   - MAX(col) - 返回最大值
   - MIN(col) - 返回最小值
   - FIRST(col) - 返回第一个记录的值
   - LAST(col) - 返回最后一个记录的值

6. 表连接--横向 join
   - 不同连接方式
   - 多张表的连接顺序
   - 条件写在 on 还是 where 之后有什么区别
      - left join
        - 使用 on 对右表限制，返回全部左边表，连接的右表内容仅保留符合 on 条件部分
        - 使用 where 对右表限制，返回左边表连接右表后，仅保留满足 where 条件部分
      - right join
        - 使用 on 对左表限制，返回全部右边表，连接的左表内容仅保留符合 on 条件部分
        - 使用 where 对左表限制，返回右边表连接左表后，仅保留满足 where 条件部分
      - inner join/join
        - 使用 on 对右表限制，连接的右表内容仅保留符合 on 条件部分，之后与左边求交集
        - 使用 where 对右表限制，左右表求交接，之后仅保留满足 where 条件部分
      - outer join
        - MySQL 不支持 OUTER JOIN，可以对左连接和右连接的结果做 UNION 操作来实现.

7. 纵向 union all、union。 Union 可去重.

8. 代码优化
   - 多表连接：先写 where 条件切一刀，然后再 join
   - 避免使用 count(distinct col)
   - 尽量将 or 转换为 union all
   - 使用 exists 代替 in

9. 窗口函数
   - 1. 排序函数
      - row_number()：序号不重复，序号连续
      - rank()：序号可以重复，序号不连续
      - dense_rank()：序号可以重复，序号连续
   - 2. 聚合函数
      - sum(列) (partition by a order by b)
   - 3. 分布函数
      - percent_rank() = (分组内当前行的 RANK 值-1) / (分组内总行数-1)
      - cume_dist() = 小于等于当前值的行数 / 分组内总行数
   - 4. 前后函数
      - lag(expression, n): 返回当前行的前 n 行
      - lead(expression, n): 返回当前行的后 n 行

10. 多表联动---子查询
    - 标量子查询：返回1行1列一个值
    - 行级子查询：返回的结果集是 1 行 N 列
    - 列级子查询：返回的结果集是 N 行 1 列
    - 表子查询：返回的结果集是 N 行 N 列

11. 表结构转置
    - 行转列
    - 列转行

12. 一对多的查询结果如何处理
   - group_concat()
