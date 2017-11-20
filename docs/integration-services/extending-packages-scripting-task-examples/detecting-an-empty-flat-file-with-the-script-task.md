---
title: "检测 with the Script Task 的空平面文件 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-task-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 40deae6a08a597114fbc721271a789895e1d8fa2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>使用脚本任务检测空平面文件
  平面文件源在尝试处理平面文件之前不确定该平面文件是否包含数据行。 您可能希望跳过不含任何数据行的文件，从而提高包的效率，尤其是循环访问大量平面文件的包。 脚本任务可以在包开始处理数据流之前查找空平面文件。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下面的示例使用从方法**System.IO**命名空间以测试指定平面文件连接管理器，以确定是否该文件为空，或者它是否仅包含预期如列的非数据行中的平面文件标头文件或空的行。 该脚本先检查文件的大小，如果大小为零字节，则该文件是空的。 如果文件大小大于零，该脚本会从文件中读取行，直到没有行可读为止，或者直到行数超过预期的非数据行数为止。 如果该文件中的行数小于或等于预期的非数据行数，则认为该文件是空的。 结果将以布尔值的形式在用户变量中返回，该变量的值可用于在包控制流中进行分支跳转。 **FireInformation**方法还会显示在结果**输出**窗口[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)。  
  
#### <a name="to-configure-this-script-task-example"></a>配置此脚本任务示例  
  
1.  创建和配置名为平面文件连接管理器**EmptyFlatFileTest**。  
  
2.  创建一个名为 `FFNonDataRows` 的整数变量，并将其值设置为预期在平面文件中出现的非数据行数。  
  
3.  创建一个名为 `FFIsEmpty` 的布尔变量。  
  
4.  添加`FFNonDataRows`变量与脚本任务的**ReadOnlyVariables**属性。  
  
5.  添加`FFIsEmpty`变量与脚本任务的**ReadWriteVariables**属性。  
  
6.  在代码中，导入**System.IO**命名空间。  
  
 如果使用的是 Foreach 文件枚举器来循环访问文件，而不是使用单个平面文件连接管理器，则需要修改下面的代码，以便从存储枚举值的变量中而不是从连接管理器获取文件名和路径。  
  
### <a name="code"></a>代码  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
## <a name="see-also"></a>另请参阅  
 [脚本任务示例](../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
  
  

