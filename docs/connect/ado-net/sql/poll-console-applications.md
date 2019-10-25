---
title: 在控制台应用程序中轮询
description: 提供一个示例，演示如何使用轮询等待从控制台应用程序中完成异步命令执行。 此方法也适用于类库或其他不带用户界面的应用程序。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 4ff084d5-5956-4db1-8e18-c5a66b000882
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: e8dc5597743a277b53f36d0bfb1487a12cbd80d9
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452100"
---
# <a name="polling-in-console-applications"></a>在控制台应用程序中轮询

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

使用 ADO.NET 中的异步操作，可以在一个线程上启动耗时的数据库操作，同时在另一个线程上执行其他任务。 但在大多数情况下，最终会到达一个点，在该点上应用程序不应继续，直到数据库操作完成。 对于这种情况，轮询异步操作以确定操作是否已完成非常有用。  
  
您可以使用 <xref:System.IAsyncResult.IsCompleted%2A> 属性来确定操作是否已完成。  
  
## <a name="example"></a>示例  
以下控制台应用程序更新 AdventureWorks 示例数据库中的数据，异步完成其任务。 为了模拟长时间运行的进程，此示例在命令文本中插入一个 WAITFOR 语句。 通常情况下，你不会尝试使命令运行速度较慢，但在这种情况下这样做会使演示异步行为变得更加容易。  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Class1  
{  
    [STAThread]  
    static void Main()  
    {  
        // The WAITFOR statement simply adds enough time to   
        // prove the asynchronous nature of the command.  
  
        string commandText =  
          "UPDATE Production.Product SET ReorderPoint = " +  
          "ReorderPoint + 1 " +  
          "WHERE ReorderPoint Is Not Null;" +  
          "WAITFOR DELAY '0:0:3';" +  
          "UPDATE Production.Product SET ReorderPoint = " +  
          "ReorderPoint - 1 " +  
          "WHERE ReorderPoint Is Not Null";  
  
        RunCommandAsynchronously(  
            commandText, GetConnectionString());  
  
        Console.WriteLine("Press Enter to continue.");  
        Console.ReadLine();  
    }  
  
    private static void RunCommandAsynchronously(  
      string commandText, string connectionString)  
    {  
        // Given command text and connection string, asynchronously  
        // execute the specified command against the connection.   
        // For this example, the code displays an indicator as it's   
        // working, verifying the asynchronous behavior.   
        using (SqlConnection connection =  
          new SqlConnection(connectionString))  
        {  
            try  
            {  
                int count = 0;  
                SqlCommand command =   
                    new SqlCommand(commandText, connection);  
                connection.Open();  
  
                IAsyncResult result =   
                    command.BeginExecuteNonQuery();  
                while (!result.IsCompleted)  
                {  
                    Console.WriteLine(  
                                    "Waiting ({0})", count++);  
                    // Wait for 1/10 second, so the counter  
                    // doesn't consume all available   
                    // resources on the main thread.  
                    System.Threading.Thread.Sleep(100);  
                }  
                Console.WriteLine(  
                    "Command complete. Affected {0} rows.",  
                command.EndExecuteNonQuery(result));  
            }  
            catch (SqlException ex)  
            {  
                Console.WriteLine("Error ({0}): {1}",   
                    ex.Number, ex.Message);  
            }  
            catch (InvalidOperationException ex)  
            {  
                Console.WriteLine("Error: {0}", ex.Message);  
            }  
            catch (Exception ex)  
            {  
                // You might want to pass these errors  
                // back out to the caller.  
                Console.WriteLine("Error: {0}", ex.Message);  
            }  
        }  
    }  
  
    private static string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,              
        // you can retrieve it from a configuration file.   
  
        // If you have not included "Asynchronous Processing=true"  
        // in the connection string, the command will not be able  
        // to execute asynchronously.  
        return "Data Source=(local);Integrated Security=SSPI;" +  
        "Initial Catalog=AdventureWorks; " +   
        "Asynchronous Processing=true";  
    }  
}  
```  
  
## <a name="next-steps"></a>后续步骤
- [异步操作](asynchronous-operations.md)
