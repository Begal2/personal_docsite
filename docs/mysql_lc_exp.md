# LeetCode刷题经验总结

1. **聚合函数**
   - `SUM()` 和 `GROUP BY` 要配合使用。例如，列转行时要使用聚合函数，因为 `GROUP BY` 之后返回的是多条记录，需要使用聚合函数将多变为一。 [例题链接](https://leetcode.cn/problems/reformat-department-table/?envType=list&envId=ZnYUKxOV)
   - 行转列使用 `UNION`

2. **`UNION` 的使用**
   - `UNION` 可以查重两个表；`UNION ALL` 不会去重。 [例题链接](https://leetcode.cn/problems/primary-department-for-each-employee/?envType=list&envId=ZnYUKxOV)

3. **合并表时的方法**
   - 可以考虑使用 `JOIN`、`UNION`、`CROSS JOIN`，或者直接从两个表中选择并分别赋予别名。

4. **使用 `GROUP BY` 时的注意事项**
   - 如果在字句中使用 `GROUP BY`，会返回多条结果并导致错误。

5. **条件控制**
   - 可以考虑使用 `IF(expression, 1, 2)` 和 `CASE WHEN THEN END` 进行条件控制。条件语句可以写在 `SELECT` 子句中。

6. **正则表达式控制字符串**
   - 使用 `column_name REGEXP ''` 进行正则表达式控制。 [例题链接](https://leetcode.cn/problems/find-users-with-valid-e-mails/)

7. **LIMIT 和 ORDER BY 的使用**
   - 使用 `LIMIT n` 返回从上至下的前 `n` 条结果。与 `ORDER BY` 配合使用。

8. **处理类似雇员和经理ID的情况**
   - 多数情况下，需要建立两个表，使用ID相等的情况进行解答。

9. **条件不适合使用 WHERE 时**
   - 可以考虑使用 `IF` 和聚合函数进行配合。

10. **返回单一值时的建议**
    - 需要返回单一值时，建议使用 `WHERE` 进行条件控制。

11. **IN 语法的注意事项**
    - `IN` 语法前面可以有两个字段，超过一个字段需要用括号包起来，不然会报错。 [例题链接](https://leetcode.cn/problems/department-highest-salary/)

12. **与偏移量有关的窗口函数 `LEAD()` 和 `LAG()`**
    - `LEAD(field, num, defaultvalue)` 用于查找后面的行，`LAG()` 用于查找前面的行。 [例题链接](https://leetcode.cn/problems/exchange-seats/submissions/), [例题链接](https://leetcode.cn/problems/restaurant-growth/)

13. **开窗函数的累积和**
    - 使用开窗函数累积和，利用 `SUM` 作为限制条件，返回新的表。 [例题链接](https://leetcode.cn/problems/last-person-to-fit-in-the-bus/)

14. **GROUP BY 只返回一组数据时的处理**
    - 考虑在 `GROUP BY` 中再加入一个分组。

15. **判断值在某一列中是否唯一**
    - 使用 `GROUP BY` 和 `COUNT` 进行判断。

16. **窗口函数详解视频**
    - [窗口函数详解视频链接](https://www.bilibili.com/video/BV1b34y147Re/?spm_id_from=333.999.0.0&vd_source=54ae30561f197f026ae06ddc3b87bbfd)

17. **排名类窗口函数命名规则**
    - 排名类窗口函数的命名需要加双引号。

18. **GROUP BY 的坑**
    - [避免 GROUP BY 坑的例题链接](https://leetcode.cn/problems/product-sales-analysis-iii/solution/chang-gui-jie-fa-yu-chang-kou-han-shu-ne-nwa4/)，原因是 `GROUP BY` 作用的只有分组列和聚合函数列，其他列不起作用，返回的其他列只有对应的第一行。

19. **表连接和 WHERE/ON 的考察**
    - 考察表连接和条件控制。 [例题链接](https://leetcode.cn/problems/market-analysis-i/)

20. **时间差计算函数 `TIMESTAMPDIFF()`**
    - 用于计算时间差，可以精确到秒。

21. **开窗函数的框架限定**
    - `ROWS n PRECEDING`：从当前行到前 `n` 行（一共 `n+1` 行）
    - `RANGE/ROWS BETWEEN` 边界规则1 AND 边界规则2：`RANGE` 表示按照值的范围进行定义框架，`ROWS` 表示按行的范围进行定义框架
    - `ROWS BETWEEN 2 PRECEDING AND 2 FOLLOWING`：当前行往前2行 + 当前行 + 当前行往后2行（一共5行）
    - `ROWS BETWEEN 1 FOLLOWING AND 3 FOLLOWING`：当前行的后1行到后3行（共3行）
    - `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`：从第一行到当前行

22. **`CASE WHEN` 语句**
    - 注意每一行内没有逗号。

23. **末尾的 `GROUP BY` 可以直接使用前面 `SELECT` 到的列。

24. **日期函数 `DATEDIFF()` 和 `TIMESTAMPDIFF()`**
    - `DATEDIFF()` 计算前面参数 - 后面参数，`TIMESTAMPDIFF()` 计算后面参数 - 前面参数。不要搞反了。

25. **排序窗口函数如 `DENSE_RANK()`**
    - 括号里不可传参。

26. **GROUP BY 的常见报错**
    - 常见错误信息：`Expression #3 of SELECT list is not in GROUP BY clause and contains nonaggregated column...` 表示 `SELECT` 语句中包含没有被 `GROUP BY` 的列。

27. **求同时在线最高瞬时用户数的方法**
    - 一般分为三步走：1）取用户进入直播间，赋值 `uv` 为1；2）取用户离开直播间，赋值 `uv` 为-1；3）使用窗口函数计算直播间的瞬时用户数；4）取各个直播间的瞬时最大值。 [详细方法](https://blog.nowcoder.net/n/dce3d99edce44c26a2e7d51e317a4adb?f=comment)

28. **`COALESCE()` 函数**
    - 返回从左至右的第一个非空值。

29. **有聚合函数就得有 `GROUP BY`**

30. **分组和窗口函数**
    - 分组不要总想着 `GROUP BY`，窗口函数也可以。

31. **窗口函数的括号**
    - 窗口函数的括号要将 `ROWS` 或 `RANGE` 也包含进去。

32. **`>=` 和 `<=` 符号的注意事项**
    - 这两个符号要挨着写，否则会报错。

33. **连续天数问题的解决**
    - 使用排名类窗口函数排序，将序列与日期做差，再使用差值确定分组。

34. **多对多关系的列处理**
    - 列之间是多对多关系时，可以直接对这些列进行分组。

35. **日期格式化函数 `DATE_FORMAT()`**
    - 注意大小写，例如 `DATE_FORMAT(dt, '%Y-%m-%d')`。

36. **留存率问题**
    - 一般可以使用左连接，这样第二天的数据如果缺少就会是 `NULL` 值。

37. **使用 `WITH` 创建临时表**
    - 使用 `WITH alias AS (...)` 可以创建临时表。

38. **留存率问题的处理**
    - 新建两个表，分别是注册表和并联登录登出表，利用 `LEFT JOIN` 返回空值计算比例。 [例题链接](https://www.nowcoder.com/practice/1fc0e75f07434ef5ba4f1fb2aa83a450?tpId=268&tqId=2285344&ru=/exam/oj&qru=/ta/sql-factory-interview/question-ranking&sourceUrl=/exam/oj?page=1&tab=SQL%E7%AF%87&topicId=268)

39. **日期函数 `DATEDIFF()` 的注意事项**
    - 较大日期写在第一个参数中。在写 `DATEDIFF` 时带有 `SELECT` 子句时，注意括号的数量。

40. **多个条件并行限制时的处理**
    - 可以考虑使用 `WHERE (para1, para2, ...)` 进行限制。 [例题链接](https://www.nowcoder.com/practice/d15ee0798e884f829ae8bd27e10f0d64?tpId=268&tqId=2286131&ru=/exam/oj&qru=/ta/sql-factory-interview/question-ranking&sourceUrl=/exam/oj?page=1&tab=SQL%E7%AF%87&topicId=268)
