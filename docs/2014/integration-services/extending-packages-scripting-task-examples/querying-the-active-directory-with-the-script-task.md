---
title: 使用脚本任务查询 Active Directory | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Active Directory access
- SSIS Script task, Active Directory access
- Script task [Integration Services], examples
- Active Directory [Integration Services]
ms.assetid: a88fefbb-9ea2-4a86-b836-e71315bac68e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c60d7954d0ecd0c7201885e7128b75ddc46aa53b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368949"
---
# <a name="querying-the-active-directory-with-the-script-task"></a>使用脚本任务查询 Active Directory
  企业数据处理应用程序（如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包）通常需要根据 Active Directory 中存储的雇员的级别、职务或其他特征来以不同方式处理数据。 Active Directory 是一个 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 目录服务，它不仅提供集中存储有关用户的元数据，还可以提供集中存储有关其他组织资产（如计算机和打印机）的元数据。 Microsoft .NET Framework 中的 `System.DirectoryServices` 命名空间提供使用 Active Directory 的类，以帮助您根据 Active Directory 中存储的信息来定向数据处理工作流。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下面的示例基于 `email` 变量的值（包含雇员的电子邮件地址），从 Active Directory 检索雇员的姓名、职务和电话号码。 包中的优先约束可使用检索到的信息，例如基于雇员的职务来确定发送具有低优先级的电子邮件消息，还是具有高优先级的页。  
  
#### <a name="to-configure-this-script-task-example"></a>配置此脚本任务示例  
  
1.  创建三个字符串变量：`email`、`name` 和 `title`。 输入一个有效的企业电子邮件地址作为 `email` 变量的值。  
  
2.  上**脚本**页**脚本任务编辑器**，将添加`email`变量`ReadOnlyVariables`属性。  
  
3.  将 `name` 和 `title` 变量添加到 `ReadWriteVariables` 属性中。  
  
4.  在脚本项目中，添加对 `System.DirectoryServices` 命名空间的引用。  
  
5.  . 在您的代码中，使用 `Imports` 语句导入 `DirectoryServices` 命名空间。  
  
> [!NOTE]  
>  若要成功运行此脚本，您的企业必须在其网络中使用 Active Directory，并在其中存储此示例使用的雇员信息。  
  
### <a name="code"></a>代码  
  
```vb  
Public Sub Main()  
  
    Dim directory As DirectoryServices.DirectorySearcher  
    Dim result As DirectoryServices.SearchResult  
    Dim email As String  
  
    email = Dts.Variables("email").Value.ToString  
  
    Try  
        directory = New _  
            DirectoryServices.DirectorySearcher("(mail=" & email & ")")  
        result = directory.FindOne  
        Dts.Variables("name").Value = _  
            result.Properties("displayname").ToString  
        Dts.Variables("title").Value = _  
            result.Properties("title").ToString  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
public void Main()  
{  
    //  
    DirectorySearcher directory;  
    SearchResult result;  
    string email;  
  
    email = (string)Dts.Variables["email"].Value;  
  
    try  
    {  
        directory = new DirectorySearcher("(mail=" + email + ")");  
        result = directory.FindOne();  
        Dts.Variables["name"].Value = result.Properties["displayname"].ToString();  
        Dts.Variables["title"].Value = result.Properties["title"].ToString();  
        Dts.TaskResult = (int)ScriptResults.Success;  
    }  
    catch (Exception ex)  
    {  
        Dts.Events.FireError(0, "Script Task Example", ex.Message + "\n" + ex.StackTrace, String.Empty, 0);  
        Dts.TaskResult = (int)ScriptResults.Failure;  
    }  
  
}  
```  
  
## <a name="external-resources"></a>外部资源  
  
-   social.technet.microsoft.com 上的技术文章，[在 SSIS 中处理 Active Directory 信息](https://go.microsoft.com/fwlink/?LinkId=199588)。  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
