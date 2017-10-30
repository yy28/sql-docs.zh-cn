---
title: "保存并运行包 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 40b8677cddf363e8789a2fc15b1c2aab5f49f58c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>保存并运行包 （SQL Server 导入和导出向导）
  在你指定并配置数据源和目标之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“保存并运行包” 。 在此页上，你可以指定是否要立即运行复制操作。 根据您的配置，你还可能无法保存您设置保存为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) 包以自定义它并以后重复使用它。
  
**什么是包？** 向导使用 SQL Server Integration Services (SSIS) 复制数据。 在 SSIS 中，基本单位是包。 当你在向导的各个页面之间移动并指定选项时，向导会在内存中创建 SSIS 包。
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>“保存并运行包”页面的屏幕截图  
下面的屏幕截图显示了向导的“保存并运行包”  页。 
   
![保存并运行导入和导出向导的包页面](../../integration-services/import-export-data/media/save-and-run.png "保存并运行导入和导出向导的包页面") 
  
## <a name="run-and-save-the-package"></a>运行并保存包 
 若要继续，必须选择以下两个选项中的至少一个。  
  
 **Run immediately**  
 选择此选项以导入和立即导出数据。 默认情况下，选中此复选框，并且该操作立即运行。
  
 **保存 SSIS 包**  
 将你的设置保存为 SSIS 包。 稍后可以根据需要自定义包，并再次运行。 如果选择保存包，下一页（“保存 SSIS 包” ）提供了一些附加选项。
 
只有在安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 标准版或更高版本时，才会提供用于保存包的选项。   
  
> [!NOTE]
> 如果完成向导，运行此操作，但停止完成运行的操作之前，不保存包，即使你选择**保存 SSIS 包**复选框。  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>如果从 Visual Studio 中启动向导
如果从 Visual Studio 与 SQL Server Data Tools (SSDT) 中的 Integration Services 项目中启动该向导：
-   你不能**运行**包后退出该向导之前。 然后你可以从 Visual Studio 运行包。
-   向导**将保存**从其中启动该向导的 Integration Services 项目中的包。

## <a name="specify-options-for-saving-the-package"></a>指定用于保存包的选项
**SQL Server**  
 选择此选项以将包保存在 SQL Server 中**msdb**数据库中**sysssispackages**表。
 
> [!IMPORTANT]
> 此选项不会将包保存到 SSIS 目录数据库 (SSISDB)。  

 在下一页（“保存 SSIS 包” ），选择目标服务器并提供凭据以连接到该服务器。 有关详细信息，请参阅 [保存 SSIS 包](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)。  
  
 **文件系统**  
 选择此选项以将包另存为的文件**.dtsx**扩展。  
  
 在下一页（“保存 SSIS 包” ），选择包的目标文件夹和文件名。 有关详细信息，请参阅 [保存 SSIS 包](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="specify-the-package-protection-level"></a>指定包保护级别
 **包保护级别**  
 从该列表中选择某个保护级别来帮助保护包中的数据。  
  
 保护级别决定保护包时所使用的方法、密码或用户密钥以及作用域。 可以保护所有数据，也可以只保护敏感数据。 有关可用选项的详细信息，请参阅 [对包中敏感数据的访问控制](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)。  
  
 **密码**  
 键入密码。  
  
 **重新键入密码**  
 再次键入该密码。  
  
> [!NOTE]
> 有密码选项仅当指定**包保护级别**，需要密码-即，如果您指定**使用密码加密敏感数据**或**使用密码加密所有数据**。  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>关于包保存选项的两个页面  
 “保存并运行包”  页是你在其上选择用于保存 SSIS 包的选项的两个页面之一。  
  
-   在当前页上，可以选择是将包保存在 SQL Server 中，还是作为文件保存。 此外，还可以选择已保存包的安全设置。  
  
-   接下来，在“保存 SSIS 包”  页上，提供包的名称以及有关其保存位置的详细信息。 有关详细信息，请参阅 [保存 SSIS 包](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)。  
  
 只有在此页上选择“保存 SSIS 包”  选项之后，这些选项才可用。  
  
## <a name="whats-next"></a>下一步是什么？  
 在指定是否要立即运行复制操作，以及是否要保存包之后，下一个页面取决于你选择的选项。  
  
-   如果选择了立即运行包但不保存它的选项，则下一个页面是“完成向导” 。 在此页上，你将查看你在向导中所做的选择，然后启动复制操作。 有关详细信息，请参阅 [完成向导](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。  
  
-   如果选择了保存包的选项，则下一个页面是“保存 SSIS 包” 。 在此页上，你将指定用于保存包的附加选项。 （然后，在保存包之后，接下来的页面是“完成向导”。）有关详细信息，请参阅[保存 SSIS 包](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)。  
  
## <a name="see-also"></a>另请参阅  
[保存包](../../integration-services/save-packages.md)  
[运行 Integration Services (SSIS) 包](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  


