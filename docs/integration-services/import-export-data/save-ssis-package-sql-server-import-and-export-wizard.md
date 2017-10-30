---
title: "保存 SSIS 包 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 6ebbab742350e6874b86213c1fbf516e095a1e9a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>保存 SSIS 包（SQL Server 导入和导出向导）
  如果在指定**保存和运行包**你想要作为 SQL Server Integration Services (SSIS) 包，保存你的设置的页[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]导入和导出向导所示**保存 SSIS 包**。 在此页上，你可以指定用于保存由向导创建的包的其他选项。  

“保存 SSIS 包”  页上显示的选项取决于你先前在“保存并运行包”  页上做出的选择（将包保存到 SQL Server 还是文件系统）。 若要再次查看“保存并运行包”  页，请参阅 [保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。
 
**什么是包？** 向导使用 SQL Server Integration Services (SSIS) 复制数据。 在 SSIS 中，基本单位是包。 当你在向导的各个页面之间移动并指定选项时，向导会在内存中创建 SSIS 包。

## <a name="screen-shot---common-options"></a>屏幕截图所示的常用选项
以下屏幕截图显示的第一部分**保存 SSIS 包**向导页。 网页的其余内容具有可变数量选项，这取决于你选择的包目标。

![保存包的常用选项](../../integration-services/import-export-data/media/save-package-common-options.png)

## <a name="provide-a-name-and-description-for-the-package"></a>提供包的名称和说明  
 **名称**  
 为包提供唯一的名称。  
  
 **描述**  
 为包提供说明。 最好说明包的用途，使其一目了然，便于维护。  
  
 **目标**  
 之前为包指定的目标（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或文件系统）。 如果要将包保存到其他目标，请返回到“保存并运行包”  页。

## <a name="screen-shot---save-the-package-in-sql-server"></a>屏幕截图 - 将包保存在 SQL Server 中

 下面的屏幕快照显示**保存 SSIS 包**如果你选择在向导页**SQL Server**选项**保存和运行包**页。 
  
![保存 SSIS 包的导入和导出向导页](../../integration-services/import-export-data/media/save-package2.png "保存 SSIS 包的导入和导出向导页")  

## <a name="options-to-specify-target--sql-server"></a>若要指定的选项 (目标 = SQL Server) 

 > [!NOTE]
 > 向导将包中的保存**msdb**数据库中**sysssispackages**表。 此选项可以完成**不**将包保存到 SSIS 目录数据库 (SSISDB)。  
 
 **服务器名称**  
 键入或选择目标服务器名称。  
   
 **使用 Windows 身份验证**  
使用 Windows 集成身份验证连接到服务器。 这是首选的身份验证方法。  
  
 **使用 SQL Server 身份验证**  
使用 SQL Server 身份验证连接到服务器。  
  
 **用户名**  
如果你指定 SQL Server 身份验证，输入的用户名。  
  
 **密码**  
如果你指定 SQL Server 身份验证，则输入的密码。  
    
## <a name="screen-shot---save-the-package-in-the-file-system"></a>屏幕截图 - 将包保存在文件系统中
 
下面的屏幕快照显示**保存 SSIS 包**如果你选择在向导页**文件系统**选项**保存和运行包**页。 
  
![保存 SSIS 包的导入和导出向导页](../../integration-services/import-export-data/media/save-package1.png "保存 SSIS 包的导入和导出向导页")  

## <a name="options-to-specify-target--file-system"></a>若要指定的选项 (目标 = 文件系统)

 **File name**  
 输入目标文件的路径和文件名，或使用**浏览**按钮以选择一个目标。  
  
> [!TIP]
> 请确保指定的目标文件夹中，通过输入它，也可以通过浏览。 如果你只需输入不含路径的文件名，你不知道该向导将包的保存。 此外，向导可能会尝试将包保存到你无权保存文件的位置，并引发错误。  
>   
>  请记住包文件的保存位置。  
  
 **浏览**  
 （可选） 通过浏览来选择中的目标文件的路径**保存包**对话框。  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>关于包保存选项的两个页面  
 “保存 SSIS 包”  页是你在其上选择用于保存 SSIS 包的选项的两个页面之一。  
  
-   在上一页（“保存并执行包” ），可以选择是将包保存在 SQL Server 中，还是作为文件保存。 此外，还可以选择已保存包的安全设置。 若要再次查看“保存并运行包”  页，请参阅 [保存并运行包](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  
  
-   在当前页上，提供包的名称以及有关其保存位置的详细信息。  
 
## <a name="run-the-saved-package-again-later"></a>稍后再次运行已保存的包  
 若要了解稍后如何再次运行已保存的包，请参阅下列主题之一。  
  
-   若要使用用户界面友好的实用工具来运行包，请参阅[执行包实用工具 (DtExecUI) UI 参考](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)。  
  
-   若要从命令行或批处理文件运行包，请参阅 [dtexec 实用工具](../../integration-services/packages/dtexec-utility.md)。  
  
-   如果包保存在 SQL Server 的 **msdb** 数据库中，请连接到 Integration Services 服务。 然后，在 SQL Server Management Studio 的对象资源管理器中，导航到“已存储的包”|“MSDB” ，右键单击该包并选择“运行包” 。

-   如果包保存在文件系统中，请参阅 [运行 Integration Services (SSIS) 包](../../integration-services/packages/run-integration-services-ssis-packages.md) 以便在开发环境中运行包。 必须将包添加到 Integration Services 项目才能打开和运行它。  

## <a name="customize-the-saved-package"></a>自定义已保存的包  
 若要了解如何自定义已保存的包，请参阅 [Integration Services (SSIS) 包](../../integration-services/integration-services-ssis-packages.md)。  
  
## <a name="whats-next"></a>下一步是什么？  
 指定用于保存包的附加选项后，下一个页面是“完成向导” 。 在此页上，你将查看你在向导中所做的选择，然后启动操作。 有关详细信息，请参阅 [完成向导](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。  
 
## <a name="see-also"></a>另请参阅  
[保存包](../../integration-services/save-packages.md)  
[运行 Integration Services (SSIS) 包](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 

