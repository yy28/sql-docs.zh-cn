---
title: "步骤 3：添加错误流重定向 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1538ad973644dfa38fbed083327528a1973bcc4e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-4-3---adding-error-flow-redirection"></a>第 4-3 课 - 添加错误流重定向
如上一个任务中所示，当 Lookup Currency Key 转换尝试对产生错误的已损坏示例平面文件进行处理时，该转换无法生成匹配。 由于转换针对错误输出使用了默认设置，因此，任何错误都将导致该转换失败。 当转换失败时，该包的其余部分也将失败。  
  
可以使用错误输出将组件配置为将失败的行重定向到其他处理路径，而不是允许转换失败。 使用单独的错误处理路径，您可以执行多项任务。 例如，您可能要尝试清除该数据，然后重新处理失败的行。 或者，您可能要将失败的行与其他错误信息保存在一起，以便以后进行验证和重新处理。  
  
在本任务中，您将 Lookup Currency Key 转换配置为将所有失败的行重定向到错误输出。 在数据流的错误分支中，这些行将被写入文件中。  
  
默认情况下， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 错误输出中的另外两列 **ErrorCode** 和 **ErrorColumn**只包含表示错误号的数值代码以及出现错误的列的 ID。 如果没有相应的错误说明，这些数值没有多大用处。  
  
若要更有效地使用错误输出，请在包将失败的行写入文件之前，使用脚本组件来访问 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] API，然后获取错误说明。  
  
## <a name="to-configure-an-error-output"></a>配置错误输出  
  
1.  在“SSIS 工具箱”中，展开“公共”，然后将“脚本组件”拖动到“数据流”选项卡的设计图面上。将“脚本”放置在“Lookup Currency Key”转换的右侧。  
  
2.  在“选择脚本组件类型”对话框中，单击“转换”，再单击“确定”。  
  
3.  单击“Lookup Currency Key”转换，并将红色箭头拖动到新添加的“脚本”转换中，以连接这两个组件。  
  
    红色箭头表示“Lookup Currency Key”转换的错误输出。 通过使用红色箭头将转换连接到脚本组件，您可以将所有处理错误重定向到脚本组件，然后，该组件会处理这些错误并将它们发送到目标。  
  
4.  在“配置错误输出”对话框的“错误”列中，选择“重定向行”，再单击“确定”。  
  
5.  在“数据流”设计图面上，在新添加的“ScriptComponent”中单击“ScriptComponent”，然后将该名称更改为Get Error Description”。  
  
6.  双击“Get Error Description”转换。  
  
7.  在“脚本转换编辑器”对话框中的“输入列”页中，选择“ErrorCode”列。  
  
8.  在“输入和输出”页中，展开“输出 0”，单击“输出列”，再单击“添加列”。  
  
9. 在“名称”属性中，键入 **ErrorDescription**并将“DataType”属性设置为“Unicode string [DT_WSTR]”。  
  
10. 在“脚本”页中，验证确保已将“LocaleID”属性设置为“英语(美国)”  
  
11. 单击“编辑脚本”打开 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA)。 在“Input0_ProcessInputRow”方法中，键入或粘贴以下代码。  
  
    [Visual Basic]  
  
    ```vb  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
    [Visual C#]  
  
    ```cs
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
    已完成的子例程如以下代码所示。  
  
    [Visual Basic]  
  
    ```vb
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
    [Visual C#]  
  
    ```cs
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. 在“生成”菜单上，单击“生成解决方案”生成脚本并保存更改，然后关闭 VSTA。  
  
13. 单击“确定”关闭“脚本转换编辑器”对话框。  
  
## <a name="next-steps"></a>后续步骤  
[步骤 4：添加平面文件目标](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
  
  
