---
title: 步骤 4： 弹性连接到使用 ADO.NET 的 SQL |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a812aacbbbd87ba8fc38479be7d62a0fc9401b6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731365"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>步骤 4：使用 ADO.NET 实现对 SQL 的弹性连接

- 上一篇文章：&nbsp;&nbsp;&nbsp;[步骤 3：使用 ADO.NET 连接到 SQL 的概念证明](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
本主题提供了演示自定义重试逻辑的 C# 代码示例。 重试逻辑提供可靠性。 重试逻辑旨在正常处理临时错误或*暂时性故障*这往往会自行消失在程序等待几秒并重试。  
  
暂时性故障的来源包括：  
  
- 支持 Internet 的网络简要失败。  
- 云系统可能是负载平衡其资源在您查询的发送时间点。  
  
  
用于连接到本地 Microsoft SQL Server 的 ADO.NET 类也可以连接到 Azure SQL 数据库。 但是，本身 ADO.NET 类不能提供的全部稳定性和可靠性有必要在生产环境中使用。 客户端程序可能会遇到暂时性故障从其应以无提示方式和正常恢复并继续进行。  
  
## <a name="step-1-identify-transient-errors"></a>步骤 1： 识别暂时性错误  
  
您的程序必须区分暂时性错误与持久性错误。 暂时性错误是时间的在短时间，如暂时性网络问题可能会清除的错误条件。  举例说明了持久错误，如果将程序具有目标数据库名称的拼写错误-"没有此类数据库找到"错误这种情况下，将仍然存在，并且没有机会的时间在短时间内清理。  
  
分类为暂时性故障的错误号的列表将在位于[SQL 数据库客户端应用程序的错误消息](http://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>步骤 2： 创建并运行示例应用程序  
  
此示例假定.NET Framework 4.5.1 或更高版本安装。  C# 代码示例包含一个名为 Program.cs 的文件。 下一节中提供其代码。  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>步骤 2.a： 捕获和编译代码示例  
  
您可以编译示例的以下步骤：  
  
1. 在中[免费的 Visual Studio 社区版](https://www.visualstudio.com/products/visual-studio-community-vs)，从 C# 控制台应用程序模板创建新项目。  
    - 文件 > 新建 > 项目 > 安装 > 模板 > Visual C# > Windows > 经典桌面 > 控制台应用程序  
    - 将项目命名**RetryAdo2**。  
2. 打开“解决方案资源管理器”窗格。  
    - 请参阅你的项目的名称。  
    - 请参阅 Program.cs 文件的名称。  
3. 打开 Program.cs 文件。  
4. 完全与下面的代码块中的代码替换 Program.cs 文件的内容。  
5. 单击生成菜单 > 生成解决方案。  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>单步 2.b： 复制和粘贴示例代码  
  
此将代码粘贴到您**Program.cs**文件。  
  
然后您必须编辑服务器名称、 密码和等等的字符串。 可以在名为方法中找到这些字符串**GetSqlConnectionStringBuilder**。  
  
注意： 服务器名称的连接字符串专门针对 Azure SQL 数据库，因为它包含的四个字符前缀**tcp:**。 但是，您可以调整要连接到 Microsoft SQL Server 的服务器字符串。  
  
  
```CSharp  
    using System;  // C#  
    using CG = System.Collections.Generic;  
    using QC = System.Data.SqlClient;  
    using TD = System.Threading;  
        
    namespace RetryAdo2  
    {  
      public class Program  
      {  
        static public int Main(string[] args)  
        {  
          bool succeeded = false;  
          int totalNumberOfTimesToTry = 4;  
          int retryIntervalSeconds = 10;  
        
          for (int tries = 1;  
            tries <= totalNumberOfTimesToTry;  
            tries++)  
          {  
            try  
            {  
              if (tries > 1)  
              {  
                Console.WriteLine  
                  ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
                  tries, totalNumberOfTimesToTry  
                  );  
                TD.Thread.Sleep(1000 * retryIntervalSeconds);  
                retryIntervalSeconds = Convert.ToInt32  
                  (retryIntervalSeconds * 1.5);  
              }  
              AccessDatabase();  
              succeeded = true;  
              break;  
            }  
        
            catch (QC.SqlException sqlExc)  
            {  
              if (TransientErrorNumbers.Contains  
                (sqlExc.Number) == true)  
              {  
                Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
                continue;  
              }  
              else  
              {  
                Console.WriteLine(sqlExc);  
                succeeded = false;  
                break;  
              }  
            }  
        
            catch (TestSqlException sqlExc)  
            {  
              if (TransientErrorNumbers.Contains  
                (sqlExc.Number) == true)  
              {  
                Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
                continue;  
              }  
              else  
              {  
                Console.WriteLine(sqlExc);  
                succeeded = false;  
                break;  
              }  
            }  
        
            catch (Exception Exc)  
            {  
              Console.WriteLine(Exc);  
              succeeded = false;  
              break;  
            }  
          }  
        
          if (succeeded == true)  
          {  
            return 0;  
          }  
          else  
          {  
            Console.WriteLine("ERROR: Unable to access the database!");  
            return 1;  
          }  
        }  
        
        /// <summary>  
        /// Connects to the database, reads,  
        /// prints results to the console.  
        /// </summary>  
        static public void AccessDatabase()  
        {  
          //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
        
          using (var sqlConnection = new QC.SqlConnection  
              (GetSqlConnectionString()))  
          {  
            using (var dbCommand = sqlConnection.CreateCommand())  
            {  
              dbCommand.CommandText = @"  
    SELECT TOP 3  
        ob.name,  
        CAST(ob.object_id as nvarchar(32)) as [object_id]  
      FROM sys.objects as ob  
      WHERE ob.type='IT'  
      ORDER BY ob.name;";  
        
              sqlConnection.Open();  
              var dataReader = dbCommand.ExecuteReader();  
        
              while (dataReader.Read())  
              {  
                Console.WriteLine("{0}\t{1}",  
                  dataReader.GetString(0),  
                  dataReader.GetString(1));  
              }  
            }  
          }  
        }  
        
        /// <summary>  
        /// You must edit the four 'my' string values.  
        /// </summary>  
        /// <returns>An ADO.NET connection string.</returns>  
        static private string GetSqlConnectionString()  
        {  
          // Prepare the connection string to Azure SQL Database.  
          var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
        
          // Change these values to your values.  
          sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
          sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
        
          sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
          sqlConnectionSB.Password = "MyPassword";  
          sqlConnectionSB.IntegratedSecurity = false;  
        
          // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
          sqlConnectionSB.ConnectRetryCount = 3;  
          sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
        
          // Leave these values as they are.  
          sqlConnectionSB.IntegratedSecurity = false;  
          sqlConnectionSB.Encrypt = true;  
          sqlConnectionSB.ConnectTimeout = 30;  
        
          return sqlConnectionSB.ToString();  
        }  
        
        static public CG.List<int> TransientErrorNumbers =  
          new CG.List<int> { 4060, 40197, 40501, 40613,  
          49918, 49919, 49920, 11001 };  
      }  
        
      /// <summary>  
      /// For testing retry logic, you can have method  
      /// AccessDatabase start by throwing a new  
      /// TestSqlException with a Number that does  
      /// or does not match a transient error number  
      /// present in TransientErrorNumbers.  
      /// </summary>  
      internal class TestSqlException : ApplicationException  
      {  
        internal TestSqlException(int testErrorNumber)  
        { this.Number = testErrorNumber; }  
        
        internal int Number  
        { get; set; }  
      }  
    }  
```  
  
###  <a name="step-2c-run-the-program"></a>单步 2.c： 运行程序  
  
  
**RetryAdo2.exe**可执行文件未输入任何参数。 若要运行.exe:  
  
1. 打开一个到已编译 RetryAdo2.exe 二进制文件的位置的控制台窗口。  
2. 运行的 RetryAdo2.exe，不带任何输入参数。  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>步骤 3： 方法可以测试重试逻辑  
  
有许多种方式来模拟暂时性错误测试重试逻辑。  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>步骤 3.a:: 引发测试异常  
  
代码示例包括：  
  
- 一个小型的第二个类，名为**TestSqlException**，一个属性名为**数**。  
- `//throw new TestSqlException(4060);` 其中可以取消注释。  
  
如果取消注释 throw 语句，并重新编译下, 一次运行**RetryAdo2.exe**输出类似于以下内容。  
  
```  
    [C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
    >> RetryAdo2.exe  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 2 of 4 max...  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 3 of 4 max...  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 4 of 4 max...  
    4060: transient occurred. (TESTING.)  
    ERROR: Unable to access the database!  
      
    [C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
    >>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>单步 3.b： 使用永久性错误重新测试  
  
要证明代码句柄一再出现的错误正确，重新运行前面的测试，但不要使用 4060 等真实暂时性错误数。 改用无意义的编号 7654321。 该程序应将此视为永久性错误，并应绕过任何重试。  
  
###  <a name="step-3c-disconnect-from-the-network"></a>单步 3.c： 从网络断开连接  
  
1. 从网络断开客户端计算机。  
    - 针对桌面、 拔出网络电缆。  
    - 对于笔记本电脑，按功能组合键关闭网络适配器。  
2. 启动 RetryAdo2.exe，并等待控制台显示的第一个暂时性错误，可能是 11001。  
3. RetryAdo2.exe 继续运行时重新连接到网络。  
4. 观看控制台报告成功在后续的重试。  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>单步 2.d： 暂时拼错服务器名称  
  
1. 暂时将 40615 添加到另一个错误号为**TransientErrorNumbers**，并重新编译。  
2. 在行上设置断点： `new QC.SqlConnectionStringBuilder()`。  
3. 使用*编辑并继续*功能特意拼错服务器名称，下面的行数。  
    - 让程序运行并回到您的断点。  
    - 发生错误 40615。  
4. 修复拼写错误。  
5. 让程序运行并成功完成。  
6. 删除 40615，并重新编译。  
  
## <a name="next-steps"></a>Next Steps  
  
若要浏览其他最佳 practicies 和设计指南，请访问[连接到 SQL 数据库： 链接、 最佳实践和设计指南](http://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
