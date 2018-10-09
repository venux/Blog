---
title: SQLServer转Oracle
comments: true
tags:
  - SQL Server
  - Oracle
categories:
  - 02.数据库
date: 2018-07-12 13:31:10
---

## 1. 情景

公司项目的新客户数据库为 Oracle，故需将项目的 SQL Server 库转换为 Oracle 库。

## 2. 工具

- SQL Server 自带的 bcm（注意：需将 SQL Server 安装目录下对应版本的 Tools\Binn 目录，如`C:\Program Files\Microsoft SQL Server\100\Tools\Binn` 添加到环境变量 Path 中）；
- [SQL Developer 17.2](http://download.oracle.com/otn/java/sqldeveloper/sqldeveloper-17.2.0.188.1159-no-jre.zip)(注意：需安装配置 Java 8)；

## 3. 代码

```C#
#region 私有方法
  /// <summary>
  /// 合并多个空格
  /// </summary>
  /// <param name="sql">源SQL</param>
  /// <returns>目标SQL</returns>
  private string MergeSpace(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      Regex replaceSpace = new Regex(@"\s{1,}", RegexOptions.IgnoreCase);
      string result = replaceSpace.Replace(sql, " ").Trim();

      return result;
  }

  /// <summary>
  /// 替换空字符串
  /// </summary>
  /// <param name="sql">源SQL</param>
  /// <returns>目标SQL</returns>
  /// <remarks>
  /// https://www.cnblogs.com/memory4young/p/use-null-empty-space-in-oracle.html
  /// 问题：Oracle中null和''(中间没空格的空字符串)是一个意思，若字段设置为非空（not null），使用''插入会报错。
  /// 解决方案：使用' '（中间多一个空格）作为空字符串
  /// </remarks>
  private string ReplaceEmptySpace(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      string result = new StringBuilder(sql).Replace("''", "' '").Replace("\"\"", "\" \"").ToString();

      return result;
  }
  
  /// <summary>
  /// 处理bool值属性情况
  /// </summary>
  /// <param name="sql">SQL</param>
  /// <returns>SQL</returns>
  /// <remarks>由于Oracle的bool值类型存为number(1)，无法实现bool和number的自动转换，故使用手动转换。</remarks>
  private string HandlerBooleanValue(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      if (sql.IndexOf("True", StringComparison.OrdinalIgnoreCase) == -1 && sql.IndexOf("False", StringComparison.OrdinalIgnoreCase) == -1)
      {
          return sql;
      }

      string result = sql;

      /**
        * 使用正则表达式的\b来区分单词边界，只匹配True、Fale，而不会匹配TrueName。
        * https://docs.microsoft.com/zh-cn/dotnet/standard/base-types/regular-expression-language-quick-reference?view=netframework-4.7.2
        */
      result = Regex.Replace(result, @"\bTrue\b", "1", RegexOptions.IgnoreCase);
      result = Regex.Replace(result, @"\bFalse\b", "0", RegexOptions.IgnoreCase);

      return result;
  }

  /// <summary>
  /// 处理SELECT语句中无FROM情况
  /// </summary>
  /// <param name="sql">源SQL</param>
  /// <returns>目标SQL</returns>
  /// <remarks>
  /// 由于Oracle必须要有FROM语句，若无，需加上FROM DUAL子句。
  /// 例子：
  /// 原：SELECT "TEST";
  /// 目标：SELECT "TEST" FROM DUAL
  /// </remarks>
  private string HandlerNotContainFromWhenSelect(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      //不是SELECT语句或已有FROM则跳过
      if (sql.IndexOf("SELECT", StringComparison.OrdinalIgnoreCase) == -1 || sql.IndexOf(" FROM", StringComparison.OrdinalIgnoreCase) != -1)
      {
          return sql;
      }

      string result = sql + " FROM DUAL";
      return result;
  }

  /// <summary>
  /// 处理当前日期函数
  /// </summary>
  /// <param name="sql"></param>
  /// <returns></returns>
  private string HandleDateOfNowFunction(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      if (sql.IndexOf("GETDATE", StringComparison.OrdinalIgnoreCase) == -1)
      {
          return sql;
      }
      string sq1 = Regex.Replace(sql, @"GETDATE\(\)", "SYSDATE", RegexOptions.IgnoreCase);

      return sq1;// Regex.Replace(sql, "GETDATE()", "SYSDATE", RegexOptions.IgnoreCase);
  }

  /// <summary>
  /// 处理日期，时间字符串
  /// </summary>
  /// <param name="sql"></param>
  /// <returns></returns>
  /// <remarks>旧代码迁移过来</remarks>
  private string HandleDateString(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      //不包括单引号和双引号，则表示无日期字符串，不处理
      if (sql.IndexOf('\'') == -1 && sql.IndexOf('"') == -1)
      {
          return sql;
      }
      //只包含一个单引号或（和）一个双引号，则表示无日期字符串，不处理
      if (sql.IndexOf('\'') == sql.LastIndexOf('\'') && sql.IndexOf('"') == sql.LastIndexOf('"'))
      {
          return sql;
      }

      string result = sql;
      int startPos = 0;

      for (int i = 0; i < result.Length; i++)
      {
          int pos = result.IndexOf('\'', startPos);

          if (pos == -1)
          {
              break;
          }

          bool isDateTime = false;

          int pos2 = result.IndexOf('\'', pos + 1);
          if (pos2 == -1)
          {
              break;
          }
          string temp = result.Substring(pos + 1, pos2 - pos - 1);
          try
          {
              string regularText = @"^(\d{1,4})(-|\/)(\d{1,2})\2(\d{1,2})";
              isDateTime = System.Text.RegularExpressions.Regex.IsMatch(temp, regularText);

              //特殊情况例如DateTime.Parse("3 333")也是可以通过的，所以要过滤

              //DateTime dt;
              //if (DateTime.TryParse(temp, out dt))
              //{
              //    if (temp.IndexOf('-') > 0 ||
              //    temp.IndexOf('/') > 0 || temp.IndexOf('\\') > 0)
              //    {
              //        isDateTime = true;
              //    }
              //}
              //else
              //    isDateTime = false;

          }
          catch (Exception)
          {
              isDateTime = false;
          }

          if (isDateTime)
          {
              result = result.Remove(pos, pos2 - pos + 1);

              string strNewDt = "";

              //根据“：”判断是否有毫秒（有3个“：”认为有毫秒）
              if (temp.Split(new string[] { ":" }, StringSplitOptions.RemoveEmptyEntries).Length > 3)
              {
                  //temp = temp.Substring(0, temp.LastIndexOf(":"));截断毫秒
                  strNewDt = "to_timestamp('" + temp + "','yyyy-mm-dd hh24:mi:ss:ff')";//转换为timestamp
                  //注意：无论是截断方式合适转换为timestamp方式，最终存储到数据库后的数据都没有毫秒
              }
              else
              {
                  strNewDt = "to_date('" + temp + "','yyyy-mm-dd hh24:mi:ss') ";
              }

              string strpre = result.Substring(0, pos);
              string strpost = result.Substring(pos);
              result = strpre + strNewDt + strpost;

              startPos = pos + strNewDt.Length;
          }
          else
              startPos = pos2 + 1;
      }

      return result;
  }

  private string ReplaceTop1(string sql)
  {
      if (sql.IndexOf("SELECT ", StringComparison.OrdinalIgnoreCase) == -1 || sql.IndexOf(" TOP ", StringComparison.OrdinalIgnoreCase) == -1)
      {
          return sql;
      }

      string result = sql;
      Dictionary<string, string> dict = new Dictionary<string, string>();
      if (this.HasChildSelect(result))
      {
          string childSql = this.GetChildSql(result);
      }
      return result;
  }

  private string ReplaceTop(string sql)
  {
      if (sql.IndexOf("SELECT ", StringComparison.OrdinalIgnoreCase) == -1 || sql.IndexOf(" TOP ", StringComparison.OrdinalIgnoreCase) == -1)
      {
          return sql;
      }

      string result = sql;
      Dictionary<string, string> dict = new Dictionary<string, string>();
      while (this.HasChildSelect(result))
      {
          string childSql = this.GetChildSql(result);
          string guid = Guid.NewGuid().ToString();
          dict.Add(guid, childSql);

          result = result.Replace(childSql, guid);
      }
      result = this.HandleTopSyntax(result);

      if (dict.Count > 0)
      {
          foreach (var di in dict)
          {
              string newValue = ReplaceTop(di.Value);
              result = result.Replace(di.Key, newValue);
          }
      }

      return result;
  }

  /// <summary>
  /// 判断sql语句中是否存在子查询
  /// </summary>
  /// <param name="sql">要判断是否存在子查询的sql语句</param>
  /// <returns>存在子查询返回true，否则返回false</returns>
  private bool HasChildSelect(string sql)
  {
      bool b = false;
      if (!string.IsNullOrEmpty(sql))
      {
          string tmpSql = sql;
          //此算法认为子查询都由“（）”括号括起来，如（select * from tableName）,注意可能会有Union方法不出现“（）”，此处未兼容
          string[] ss = tmpSql.ToUpper().Split(new string[] { "SELECT" }, StringSplitOptions.RemoveEmptyEntries);
          if (ss != null && ss.Length > 0)
          {
              foreach (string s in ss)
              {
                  if (s.Trim().EndsWith("("))
                  {
                      b = true;
                      break;
                  }
              }
          }
      }
      return b;
  }

  /// <summary>
  /// 获取子查询语句
  /// </summary>
  /// <param name="sql">原sql语句</param>
  /// <returns>子查询sql</returns>
  private string GetChildSql(string sql)
  {
      string tmpSql = sql;
      //此算法认为子查询都由“（）”括号括起来，如（select * from tableName）,注意可能会有Union方法不出现“（）”，此处未兼容
      int startIndex = 0;//截取子查询的开始索引
      int selectIndex = tmpSql.IndexOf("SELECT ", 0, StringComparison.OrdinalIgnoreCase);
      while (selectIndex != -1)
      {
          startIndex += selectIndex;
          if (tmpSql.Substring(0, selectIndex).Trim().EndsWith("("))
          {
              break;
          }
          else
          {
              tmpSql = tmpSql.Substring(selectIndex + 6);
              selectIndex = tmpSql.IndexOf("SELECT ", 0, StringComparison.OrdinalIgnoreCase);
          }
      }
      int endIndex = startIndex;//截取子查询的结束索引
      int tmp = 0;//记录左括号数量
      for (int i = startIndex; i < tmpSql.Length; i++)
      {
          if (tmpSql[i] == ')')
          {
              if (tmp == 0)
              {
                  endIndex = i;
                  break;
              }
              else
              {
                  tmp--;
              }
          }
          else if (tmpSql[i] == '(')
          {
              tmp++;
          }
      }
      tmpSql = tmpSql.Substring(startIndex, endIndex - startIndex);
      return tmpSql;
  }

  ///处理TOP语法
  /// </summary>
  /// <param name="sql"></param>
  /// <returns></returns>
  /// <remarks>旧代码迁移过来</remarks>
  private string HandleTopSyntax(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      if (sql.IndexOf("SELECT ", StringComparison.OrdinalIgnoreCase) == -1 || sql.IndexOf(" TOP ", StringComparison.OrdinalIgnoreCase) == -1)
      {
          return sql;
      }

      string result = sql;

      //若有TOP，则前方需有SELECT，故从第六个字符开始搜索
      int topIndex = sql.IndexOf(" TOP ", 6, StringComparison.OrdinalIgnoreCase);

      sql = sql.Substring(topIndex + 4);
      result = result.Substring(topIndex + 4);

      sql = sql.Trim();
      result = result.Trim();

      //具体条数
      string count = sql.Substring(0, sql.IndexOf(' '));

      sql = sql.Substring(sql.IndexOf(' '));
      result = result.Substring(result.IndexOf(' '));

      result = "SELECT " + result;
      int whereIndex = result.LastIndexOf("WHERE", StringComparison.OrdinalIgnoreCase);
      if (whereIndex > 0)
      {
          result = result.Insert(whereIndex + 5, " ROWNUM<= " + count + " AND ");
      }
      else
      {
          int orderbyIndex = result.LastIndexOf("ORDER BY", StringComparison.OrdinalIgnoreCase);
          if (orderbyIndex > 0)
          {
              //result = result.Insert(orderbyIndex, " WHERE ROWNUM<= " + count);
              //Oracle中先执行ORDER BY，后再外层执行条数选择
              //result = "SELECT * FROM (" + result + " ) WHERE ROWNUM <= " + count;
          }
          else
          {
              result = result + " WHERE ROWNUM<= " + count;
          }
      }

      return result;
  }

  /// <summary>
  /// lfc改造后的方法，外层包Select后引起原原sql中存在select * 时报错
  /// </summary>
  /// <param name="sql"></param>
  /// <returns></returns>
  /// <remarks>旧代码迁移过来</remarks>
  private string HandleTopSyntax_LFC(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      if (sql.IndexOf("SELECT ", StringComparison.OrdinalIgnoreCase) == -1 || sql.IndexOf(" TOP ", StringComparison.OrdinalIgnoreCase) == -1)
      {
          return sql;
      }

      string result = sql;

      //若有TOP，则前方需有SELECT，故从第六个字符开始搜索
      int topIndex = result.IndexOf(" TOP ", 6, StringComparison.OrdinalIgnoreCase);

      //sql = sql.Substring(topIndex + 4);
      result = result.Substring(topIndex + 4).Trim();

      //sql = sql.Trim();
      //result = result.Trim();

      //获取Top值
      string count = result.Substring(0, result.IndexOf(' '));

      //sql = sql.Substring(sql.IndexOf(' '));
      result = result.Substring(result.IndexOf(' '));//获取top N后的sql部分

      result = "SELECT * FROM (SELECT " + result;
      //int whereIndex = result.LastIndexOf("WHERE", StringComparison.OrdinalIgnoreCase);
      //if (whereIndex > 0)
      //{
      //    //result = result.Insert(whereIndex + 5, " ROWNUM<= " + count + " AND ");
      //}
      //else
      //{
      //    int orderbyIndex = result.LastIndexOf("ORDER BY", StringComparison.OrdinalIgnoreCase);
      //    if (orderbyIndex > 0)
      //    {
      //        //result = result.Insert(orderbyIndex, " WHERE ROWNUM<= " + count);
      //        //Oracle中先执行ORDER BY，后再外层执行条数选择
      //        result = "SELECT * FROM (" + result + " ) WHERE ROWNUM <= " + count;
      //    }
      //    else
      //    {
      //        result = result + " WHERE ROWNUM<= " + count;
      //    }
      //}

      result = result + ") WHERE ROWNUM<= " + count;

      return result;
  }

  /// <summary>
  /// 处理Worklist
  /// </summary>
  /// <param name="sql"></param>
  /// <returns></returns>
  /// <remarks>
  /// 旧代码迁移过来
  /// 备注：
  /// 由于Oracle字段名最大长度为30个，而SQL Server的Recycle_Worklist和Worklist表中有字段名超出30个，故单独修改Oracle部分字段的字段名以兼容ORACLE。
  /// 查询字段名大于30字符的SQL：
  /// SELECT
  ///     sysobjects.name AS TableName,
  ///     syscolumns.name AS ColumnName,
  ///     UPPER(syscolumns.name) AS OracleColumnName
  /// FROM
  ///     sysobjects
  ///     LEFT JOIN syscolumns ON syscolumns.id= sysobjects.id 
  /// WHERE
  ///     sysobjects.xtype= 'u' 
  ///     AND len( syscolumns.name ) > 30 
  /// ORDER BY
  ///     TableName ASC,
  ///     ColumnName ASC;
  /// </remarks>
  private string HandleWorkList(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      if (sql.IndexOf("Worklist", StringComparison.OrdinalIgnoreCase) == -1)
      {
          return sql;
      }

      string result = sql;

      result = Regex.Replace(result, "ScheduledProcedureStepStartDate", "SpsStartDate", RegexOptions.IgnoreCase);
      result = Regex.Replace(result, "ScheduledProcedureStepStartTime", "SpsStartTime", RegexOptions.IgnoreCase);
      result = Regex.Replace(result, "ScheduledPerformingPhysiciansName", "ScheduledPerfPhysiciansName", RegexOptions.IgnoreCase);
      result = Regex.Replace(result, "ScheduledPerformingPhysiciansChineseName", "ScheduledPerfPhysiciansChName", RegexOptions.IgnoreCase);
      result = Regex.Replace(result, "ScheduledActionItemCodingSchemeDesignator", "SpsItemDesignator", RegexOptions.IgnoreCase);
      result = Regex.Replace(result, "Confidentialityconstraintonpatientdata", "ConfConstraintPatData", RegexOptions.IgnoreCase);
      result = Regex.Replace(result, "ScheduledProcedureStepDescription", "SpsDescription", RegexOptions.IgnoreCase);

      return result;
  }

  /// <summary>
  /// 处理方括号
  /// </summary>
  /// <param name="sql"></param>
  /// <returns></returns>
  /// <remarks>旧代码迁移过来</remarks>
  private string HandleSquareBracket(string sql)
  {
      if (string.IsNullOrEmpty(sql))
      {
          return sql;
      }

      if (sql.Contains("[") == false && sql.Contains("]") == false)
      {
          return sql;
      }

      string result = sql;

      result = result.Replace("[", string.Empty);
      result = result.Replace("]", string.Empty);

      return result;
  }

  #region 旧代码
  private string ConvertToOracleSyntax(string sql)
  {
      string oracleSyntax = sql.Trim();
      sql = sql.ToLower().Trim();
      int startPos = 0;

      #region SELECT TOP语法转换
      if (sql.Substring(0, 6) == "select")
      {
          int topIndex = sql.IndexOf(" top ");
          if (topIndex >= 6 && topIndex < 10)
          {
              sql = sql.Substring(topIndex + 4);
              oracleSyntax = oracleSyntax.Substring(topIndex + 4);

              sql = sql.Trim();
              oracleSyntax = oracleSyntax.Trim();

              string nstr = sql.Substring(0, sql.IndexOf(' '));

              sql = sql.Substring(sql.IndexOf(' '));
              oracleSyntax = oracleSyntax.Substring(oracleSyntax.IndexOf(' '));

              oracleSyntax = "select " + oracleSyntax;
              oracleSyntax = oracleSyntax.ToUpper();
              int whereIndex = oracleSyntax.LastIndexOf("WHERE");
              if (whereIndex > 0)
              {
                  oracleSyntax = oracleSyntax.Insert(whereIndex + 5, " ROWNUM<= " + nstr + " AND ");
              }
              else
              {
                  int orderbyIndex = oracleSyntax.LastIndexOf("ORDER BY");
                  if (orderbyIndex > 0)
                  {
                      oracleSyntax = oracleSyntax.Insert(orderbyIndex, " WHERE ROWNUM<= " + nstr);
                  }
                  else
                  {
                      oracleSyntax = oracleSyntax + " WHERE ROWNUM<= " + nstr;
                  }
              }

              //oracleSyntax = "select * from ( select " + oracleSyntax + " ) where rownum <= " + nstr;
          }
      }
      #endregion

      #region 时间格式转换
      //to_date
      for (int i = 0; i < oracleSyntax.Length; i++)
      {
          int pos = oracleSyntax.IndexOf('\'', startPos);
          bool isDateTime = false;
          if (pos >= 0)
          {
              int pos2 = oracleSyntax.IndexOf('\'', pos + 1);
              if (pos2 > 0)
              {
                  string temp = oracleSyntax.Substring(pos + 1, pos2 - pos - 1);
                  try
                  {
                      string regularText = @"^(\d{1,4})(-|\/)(\d{1,2})\2(\d{1,2})";
                      isDateTime = System.Text.RegularExpressions.Regex.IsMatch(temp, regularText);

                      //特殊情况例如DateTime.Parse("3 333")也是可以通过的，所以要过滤

                      //DateTime dt;
                      //if (DateTime.TryParse(temp, out dt))
                      //{
                      //    if (temp.IndexOf('-') > 0 ||
                      //    temp.IndexOf('/') > 0 || temp.IndexOf('\\') > 0)
                      //    {
                      //        isDateTime = true;
                      //    }
                      //}
                      //else
                      //    isDateTime = false;

                  }
                  catch (Exception)
                  {
                      isDateTime = false;
                  }

                  if (isDateTime)
                  {
                      oracleSyntax = oracleSyntax.Remove(pos, pos2 - pos + 1);
                      string strNewDt = "to_date('" + temp + "','yyyy-mm-dd hh24:mi:ss') ";

                      string strpre = oracleSyntax.Substring(0, pos);
                      string strpost = oracleSyntax.Substring(pos);
                      oracleSyntax = strpre + strNewDt + strpost;

                      startPos = pos + strNewDt.Length;
                  }
                  else
                      startPos = pos2 + 1;
              }
              else
              {
                  break;
              }
          }
          else
          {
              break;
          }
      }
      #endregion

      if (oracleSyntax.IndexOf(" Worklist") > 0)
      {
          oracleSyntax = oracleSyntax.Replace("ScheduledProcedureStepStartDate", "SpsStartDate");
          oracleSyntax = oracleSyntax.Replace("ScheduledProcedureStepStartTime", "SpsStartTime");
          oracleSyntax = oracleSyntax.Replace("ScheduledPerformingPhysiciansName", "ScheduledPerfPhysiciansName");
          oracleSyntax = oracleSyntax.Replace("ScheduledPerformingPhysiciansChineseName", "ScheduledPerfPhysiciansChName");
          oracleSyntax = oracleSyntax.Replace("ScheduledActionItemCodingSchemeDesignator", "SpsItemDesignator");
          oracleSyntax = oracleSyntax.Replace("Confidentialityconstraintonpatientdata", "ConfConstraintPatData");
          oracleSyntax = oracleSyntax.Replace("ScheduledProcedureStepDescription", "SpsDescription");
      }
      oracleSyntax = oracleSyntax.Replace("[", string.Empty);
      oracleSyntax = oracleSyntax.Replace("]", string.Empty);

      return oracleSyntax;
  }
  #endregion

  #endregion
```

### 参考

- [Migrating a Microsoft SQL Server Database to Oracle Database 11g](http://www.oracle.com/webfolder/technetwork/tutorials/obe/db/hol08/sqldev_migration/mssqlserver/migrate_microsoft_sqlserver_otn.htm)
- [用 SQL Developer 3.2 将 SQL Server 2008 数据库离线迁移到 Oracle 11g](https://blog.csdn.net/rootcn/article/details/8894130)
- [Oracle和sqlserver数据类型对应](https://www.cnblogs.com/benbenfishfish/p/8675075.html)
- [Oracle 和SQL Server 中的SQL语句使用区别](https://www.cnblogs.com/Jashinck/p/8652058.html)
- [sql server t-sql脚本转成oracle plsql](https://blog.csdn.net/leftfist/article/details/71133570)
- [Oracle中的NULL、’’（空字符串）以及’_’（空格）](https://www.cnblogs.com/memory4young/p/use-null-empty-space-in-oracle.html)