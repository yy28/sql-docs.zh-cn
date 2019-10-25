---
title: 步骤4：通过 ADO.NET 将弹性连接到 SQL |Microsoft Docs
description: 介绍如何将 reciliently 连接到 SQL
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: rothja
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 62ec2eb775ef5fba76b402d1871afe6c87bcc606
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451801"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>步骤 4：使用 ADO.NET 实现对 SQL 的弹性连接

![Download-DownArrow-Circled](../../ssdt/media/download.png)[下载 ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

- 上一篇文章：&nbsp;&nbsp;&nbsp;[步骤 3：使用 ADO.NET 连接到 SQL 的概念证明](step-3-connect-sql-ado-net.md)  

  
本主题提供一个用于演示自定义重试逻辑的 C# 代码示例。 重试逻辑提供可靠性。 重试逻辑旨在正常处理暂时错误或暂时性故障，在程序等待几秒并重试后，这种错误或故障往往会自行消失。  
  
暂时性故障的原因包括：  
  
- 支持 Internet 的网络短暂失败。  
- 云系统可能会在发送查询时对其资源进行负载均衡。  
  
  
用于连接本地 Microsoft SQL Server 的 ADO.NET 类也可以连接到 Azure SQL 数据库。 但是，ADO.NET 类本身无法提供生产环境中所需的稳定性和可靠性。 客户端程序可能会遇到暂时性故障，在此情况下，客户端程序应该能够自行从故障中静默正常恢复。  
  
## <a name="step-1-identify-transient-errors"></a>步骤 1：识别暂时性错误  
  
程序必须区分暂时性错误与持久性错误。 暂时性错误是一小段时间内可能会清除的错误情况，如暂时性的网络问题。  例如，如果您的程序有一个错误的目标数据库名称（在这种情况下，"找不到数据库" 错误），则可能会保留 "找不到数据库" 错误，并且不会在短时间内清除。  
  
[SQL 数据库客户端应用程序的错误消息](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)中提供了分类为暂时性故障的错误编号的列表  
  
## <a name="step-2-create-and-run-sample-application"></a>步骤2：创建并运行示例应用程序  
  
本示例假定已安装 .NET Framework 4.5.1 或更高版本。  C# 代码示例包含一个名为 Program.cs 的文件。 下一部分提供了其代码。  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>步骤 2.a：捕获和编译代码示例  
  
可以使用以下步骤编译该示例：  
  
1. 在[免费的 Visual Studio Community 版本](https://www.visualstudio.com/products/visual-studio-community-vs)中，基于 C# 控制台应用程序模板创建一个新项目。  
    - “文件”>“新建”>“项目”>“已安装”>“模板”> Visual C# > Windows >“经典桌面”>“控制台应用程序”  
    - 将该项目命名为 RetryAdo2。  
2. 打开“解决方案资源管理器”窗格。  
    - 查看项目的名称。  
    - 查看 Program.cs 文件的名称。  
3. 打开 Program.cs 文件。  
4. 将 Program.cs 文件的内容全部替换为下面的代码块中的代码。  
5. 单击菜单“生成”>“生成解决方案”。  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>步骤 2. b：复制并粘贴示例代码  
  
将此代码粘贴到你的 Program.cs 文件中。  
  
然后，你必须编辑服务器名称、密码等字符串。 你可以在名为 GetSqlConnectionStringBuilder 的方法中找到这些字符串。  
  
注意：服务器名称的连接字符串适用于 Azure SQL 数据库，因为它包含 tcp 的四个字符前缀 **：** 。 但你可以调整服务器字符串以连接到 Microsoft SQL Server。  
  
  
```csharp
using System;  // C#  
using CG = System.Collections.Generic;  
using QC = Microsoft.Data.SqlClient;  
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
  
###  <a name="step-2c-run-the-program"></a>步骤 2. c：运行程序  
  
  
RetryAdo2.exe 可执行文件未输入任何参数。 若要运行 .exe：  
  
1. 打开一个控制台窗口，在其中编译了 Retryado2.exe 二进制文件。  
2. 运行不带输入参数的 Retryado2.exe。  
  
  
  
```  
database_firewall_rules_table   245575913  
filestream_tombstone_2073058421 2073058421  
filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>步骤3：测试重试逻辑的方法  
  
可以通过多种方式来模拟暂时性错误，以测试重试逻辑。  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>步骤 3. a：引发测试异常  
  
此代码示例包括：  
  
- 名为**TestSqlException**的小型第二个类，其属性为**Number**。  
- `//throw new TestSqlException(4060);`，您可以取消注释。  
  
如果取消注释 throw 语句并重新编译，则**retryado2.exe**的下一次运行将输出类似于下面的内容。  
  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>步骤 3. b：使用永久性错误重新测试  
  
若要证明代码正确地处理持久错误，请重新运行前面的测试，但不要使用实际暂时性错误，如4060。 请改用无号数字7654321。 程序应将此视为永久性错误，并应绕过任何重试。  
  
###  <a name="step-3c-disconnect-from-the-network"></a>步骤 3. c：断开与网络的连接  
  
1. 从网络中断开客户端计算机。  
    - 对于桌面，拔下网络电缆。  
    - 对于便携式计算机，按下键的函数组合来关闭网络适配器。  
2. 启动 Retryado2.exe，并等待控制台显示第一个暂时性错误，可能为11001。  
3. 重新连接到网络，Retryado2.exe 将继续运行。  
4. 观看控制台报告成功的后续重试。  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>步骤 2. d：临时拼错服务器名称  
  
1. 暂时将40615作为另一个错误号添加到**TransientErrorNumbers**，然后重新编译。  
2. 在 `new QC.SqlConnectionStringBuilder()` 行上设置一个断点。  
3. 使用 "*编辑并继续*" 功能可以故意使服务器名称有拼写错误，如下所示。  
    - 让程序运行并返回到你的断点。  
    - 出现错误40615。  
4. 修复拼写错误。  
5. 让程序运行并成功完成。  
6. 删除40615，然后重新编译。  
  
## <a name="next-steps"></a>后续步骤  
  
若要探索其他最佳 practicies 和设计准则，请访问[连接到 SQL 数据库：链接、最佳实践和设计指南](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
