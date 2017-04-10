---
title: "保存 SSIS 包（SQL Server 导入和导出向导） | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.savedtspackage.f1"
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# 保存 SSIS 包（SQL Server 导入和导出向导）
  如果在“保存并运行包”页上指定要保存向导创建的 SSIS 包，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导将显示“保存 SSIS 包”。 在此页上，你将指定用于保存包的附加选项。  

“保存 SSIS 包”页上显示的选项取决于你先前在“保存并运行包”页上做出的选择（将包保存到 SQL Server 还是文件系统）。 若要再次查看“保存并运行包”页，请参阅[保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。
 
**什么是包？** 向导使用 SQL Server Integration Services (SSIS) 复制数据。 在 SSIS 中，基本单位是包。 当你在向导的各个页面之间移动并指定选项时，向导会在内存中创建 SSIS 包。
 
## <a name="screen-shot---save-the-package-in-the-file-system"></a>屏幕截图 - 将包保存在文件系统中
 
下面的屏幕截图显示在“保存并运行包”页上选择“文件系统”选项后向导的“保存 SSIS 包”页。 
  
![Save SSIS Package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-package1.png "Save SSIS Package page of the Import and Export Wizard")  

## <a name="screen-shot---save-the-package-in-sql-server"></a>屏幕截图 - 将包保存在 SQL Server 中

 下面的屏幕截图显示在“保存并运行包”页上选择“SQL Server”选项后向导的“保存 SSIS 包”页。 
  
![Save SSIS Package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-package2.png "Save SSIS Package page of the Import and Export Wizard")  
  
## <a name="provide-a-name-and-description-for-the-package"></a>提供包的名称和说明  
 **名称**  
 为包提供唯一的名称。  
  
 **描述**  
 为包提供说明。 最好说明包的用途，使其一目了然，便于维护。  
  
 **目标**  
 之前为包指定的目标（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或文件系统）。 如果要将包保存到其他目标，请返回到“保存并运行包”页。
  
## <a name="save-the-package-in-the-file-system"></a>将包保存在文件系统中 
如果选择了文件系统目标，请完成以下字段。

 **文件名**  
 键入目标文件的路径和文件名，或使用“浏览”按钮选择目标。  
  
> [!TIP] 务必以键入或浏览的方式指定目标文件夹。 如果仅键入文件名而不键入路径，则不知道向导将包保存在什么位置。 此外，向导可能会尝试将包保存到你无权保存文件的位置，并引发错误。  
>   
>  请记住包文件的保存位置。  
  
 **浏览**  
 （可选）通过使用“保存包”对话框浏览以选择目标文件的路径。  

## <a name="save-the-package-in-sql-server"></a>将包保存在 SQL Server 中 
如果选择了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标，请完成以下字段。

向导会将包保存在 **msdb** 数据库的 **sysssispackages** 表中。
 
 > [!NOTE] 此选项不会将包保存到 SSIS 目录数据库 (SSISDB)。  
 
 **服务器名称**  
 键入或选择目标服务器名称。  
   
 **使用 Windows 身份验证**  
使用 Windows 集成身份验证连接到服务器。 这是首选的身份验证方法。  
  
 **使用 SQL Server 身份验证**  
使用 SQL Server 身份验证连接到服务器。  
  
 **用户名**  
在指定 SQL Server 身份验证后，键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户名。  
  
 **密码**  
在指定 SQL Server 身份验证后，键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密码。  
  
## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>关于包保存选项的两个页面  
 “保存 SSIS 包”页是你在其上选择用于保存 SSIS 包的选项的两个页面之一。  
  
-   在上一页（“保存并执行包”），可以选择是将包保存在 SQL Server 中，还是作为文件保存。 此外，还可以选择已保存包的安全设置。 若要再次查看“保存并运行包”页，请参阅[保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  
  
-   在当前页上，提供包的名称以及有关其保存位置的详细信息。  
 
## <a name="run-the-saved-package-again-later"></a>稍后再次运行已保存的包  
 若要了解稍后如何再次运行已保存的包，请参阅下列主题之一。  
  
-   若要使用用户界面友好的实用工具来运行包，请参阅[执行包实用工具 (DtExecUI) UI 参考](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)。  
  
-   若要从命令行或批处理文件运行包，请参阅 [dtexec 实用工具](../../integration-services/packages/dtexec-utility.md)。  
  
-   如果包保存在文件系统中，请参阅[在 SQL Server Data Tools 中运行包](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md)以便在开发环境中运行包。 必须将包添加到 Integration Services 项目才能打开和运行它。  
 
-   如果包保存在 SQL Server 的 **msdb** 数据库中，请连接到 Integration Services 服务。 然后，在 SQL Server Management Studio 的对象资源管理器中，导航到“已存储的包”|“MSDB”，右键单击该包并选择“运行包”。

## <a name="customize-the-saved-package"></a>自定义已保存的包  
 若要了解如何自定义已保存的包，请参阅 [Integration Services (SSIS) 包](../../integration-services/integration-services-ssis-packages.md)。  
  
## <a name="whats-next"></a>下一步是什么？  
 指定用于保存包的附加选项后，下一个页面是“完成向导”。 在此页上，你将查看你在向导中所做的选择，然后启动操作。 有关详细信息，请参阅[完成向导](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。  
 
## <a name="see-also"></a>另请参阅  
[保存包](../../integration-services/save-packages.md)  
[运行 Integration Services (SSIS) 包](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 