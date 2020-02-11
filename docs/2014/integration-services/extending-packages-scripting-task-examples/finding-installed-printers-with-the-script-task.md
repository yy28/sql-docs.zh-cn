---
title: 使用脚本任务查找已安装的打印机 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- System.Drawing.Printing namespace
- printers [Integration Services]
- SSIS Script task, printers
- locating printers
- Printing namespace
- Script task [Integration Services], examples
- finding printers [SQL Server]
- Script task [Integration Services], printers
ms.assetid: 50a55014-e2c3-4ecd-84e1-3e877c55a260
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: abc0228063e62447c34b0236009977a33bddb176
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768493"
---
# <a name="finding-installed-printers-with-the-script-task"></a>使用脚本任务查找已安装的打印机
  由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包转换的数据的最终目的通常是打印成一份报表。 中`System.Drawing.Printing` [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]的命名空间提供了用于使用打印机的类。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>说明  
 以下示例查找服务器上安装的支持合法纸张大小（以在美国使用为例）的打印机。 用于检查所支持的纸张大小的代码封装在一个私有函数中。 为了能够跟踪脚本检查每个打印机设置的进度，脚本使用 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 方法对具有合法纸张大小的打印机引发信息性消息，对不具有合法纸张大小的打印机引发警告。 在设计器中运行包时，这些消息显示在 **** Tools for Applications (VSTA) IDE 的“输出”[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]窗口中。  
  
#### <a name="to-configure-this-script-task-example"></a>配置此脚本任务示例  
  
1.  创建名为 `PrinterList` 的 `Object` 类型变量。  
  
2.  在“脚本任务编辑器”**** 的“脚本”**** 页，将此变量添加到 ReadWriteVariables 属性。  
  
3.  在脚本项目中，添加对 System.Drawing**** 命名空间的引用。  
  
4.  在代码中，使用`Imports`语句导入**system.web**和`System.Drawing.Printing`命名空间。  
  
### <a name="code"></a>代码  
  
```vb  
Public Sub Main()  
  
    Dim printerName As String  
    Dim currentPrinter As New PrinterSettings  
    Dim size As PaperSize  
  
    Dim printerList As New ArrayList  
    For Each printerName In PrinterSettings.InstalledPrinters  
        currentPrinter.PrinterName = printerName  
        If PrinterHasLegalPaper(currentPrinter) Then  
            printerList.Add(printerName)  
            Dts.Events.FireInformation(0, "Example", _  
                "Printer " & printerName & " has legal paper.", _  
                String.Empty, 0, False)  
        Else  
            Dts.Events.FireWarning(0, "Example", _  
                "Printer " & printerName & " DOES NOT have legal paper.", _  
                String.Empty, 0)  
        End If  
    Next  
  
    Dts.Variables("PrinterList").Value = printerList  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Function PrinterHasLegalPaper( _  
    ByVal thisPrinter As PrinterSettings) As Boolean  
  
    Dim size As PaperSize  
    Dim hasLegal As Boolean = False  
  
    For Each size In thisPrinter.PaperSizes  
        If size.Kind = PaperKind.Legal Then  
            hasLegal = True  
        End If  
    Next  
  
    Return hasLegal  
  
End Function  
```  
  
```csharp  
public void Main()  
        {  
  
            PrinterSettings currentPrinter = new PrinterSettings();  
            PaperSize size;  
            Boolean Flag = false;  
  
            ArrayList printerList = new ArrayList();  
            foreach (string printerName in PrinterSettings.InstalledPrinters)  
            {  
                currentPrinter.PrinterName = printerName;  
                if (PrinterHasLegalPaper(currentPrinter))  
                {  
                    printerList.Add(printerName);  
                    Dts.Events.FireInformation(0, "Example", "Printer " + printerName + " has legal paper.", String.Empty, 0, ref Flag);  
                }  
                else  
                {  
                    Dts.Events.FireWarning(0, "Example", "Printer " + printerName + " DOES NOT have legal paper.", String.Empty, 0);  
                }  
            }  
  
            Dts.Variables["PrinterList"].Value = printerList;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private bool PrinterHasLegalPaper(PrinterSettings thisPrinter)  
        {  
  
            bool hasLegal = false;  
  
            foreach (PaperSize size in thisPrinter.PaperSizes)  
            {  
                if (size.Kind == PaperKind.Legal)  
                {  
                    hasLegal = true;  
                }  
            }  
  
            return hasLegal;  
  
        }  
```  
  
![Integration Services 图标（小）](../media/dts-16.gif "集成服务图标（小）")**保持与 Integration Services 最**新  <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [脚本任务示例](../extending-packages-scripting-task-examples/script-task-examples.md)  
  
  
