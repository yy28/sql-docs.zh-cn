---
title: "查询 Active Directory 与脚本任务 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Active Directory access
- SSIS Script task, Active Directory access
- Script task [Integration Services], examples
- Active Directory [Integration Services]
ms.assetid: a88fefbb-9ea2-4a86-b836-e71315bac68e
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ee5a82829785e78554b105e1f3bf3bd24f05b778
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="querying-the-active-directory-with-the-script-task"></a>使用脚本任务查询 Active Directory
  企业数据处理应用程序（如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包）通常需要根据 Active Directory 中存储的雇员的级别、职务或其他特征来以不同方式处理数据。 Active Directory 是[!INCLUDE[msCoName](../../includes/msconame-md.md)]提供集中式的存储的元数据，不仅在内的用户信息，也关于其他组织的资产，例如计算机和打印机的 Windows 目录服务。 **System.DirectoryServices** Microsoft.NET Framework 中的命名空间提供用于使用 Active Directory，以帮助你直接数据处理工作流根据它存储的信息的类。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个包的任务，请考虑以此脚本任务示例中的代码为基础，创建自定义任务。 有关详细信息，请参阅 [开发自定义任务](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下面的示例基于 `email` 变量的值（包含雇员的电子邮件地址），从 Active Directory 检索雇员的姓名、职务和电话号码。 包中的优先约束可使用检索到的信息，例如基于雇员的职务来确定发送具有低优先级的电子邮件消息，还是具有高优先级的页。  
  
#### <a name="to-configure-this-script-task-example"></a>配置此脚本任务示例  
  
1.  创建三个字符串变量：`email`、`name` 和 `title`。 输入一个有效的企业电子邮件地址作为 `email` 变量的值。  
  
2.  上**脚本**页**脚本任务编辑器**，添加`email`变量**ReadOnlyVariables**属性。  
  
3.  添加`name`和`title`到变量**ReadWriteVariables**属性。  
  
4.  在脚本项目中，添加对的引用**System.DirectoryServices**命名空间。  
  
5.  实例时都提供 SQL Server 登录名。 在代码中，使用**导入**用于导入语句**DirectoryServices**命名空间。  
  
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
  
-   技术文章[中 SSIS 处理 Active Directory 信息](http://go.microsoft.com/fwlink/?LinkId=199588)，social.technet.microsoft.com 上  
  
  

