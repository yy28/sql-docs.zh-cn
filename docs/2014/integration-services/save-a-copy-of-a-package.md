---
title: 保存包的副本 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 21482a20-e420-4452-b7eb-8f9fa1929f31
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d1a550e97bcb4cb14c56492edfa8cdd333599ecb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125120"
---
# <a name="save-a-copy-of-a-package"></a>保存一个包副本 
  此过程介绍如何将包的副本保存到文件系统、包存储区或 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 **msdb** 数据库。 指定保存包副本的位置时，也能够更新包的名称。  
  
 包存储区可以同时包括 **msdb** 数据库和文件系统中的文件夹，也可以只包含 **msdb**或文件系统中的文件夹。 在 **msdb**中，包将保存到 **sysssispackages** 表中。 此表包括一个 **folderid** 列，用于标识包所属的逻辑文件夹。 逻辑文件夹提供了对保存到 **msdb** 中的包进行分组的有用方式，文件系统中的文件夹也提供了对保存到文件系统中的包进行分组的方式。 **msdb** 中的 **sysssispackagefolders** 表中的行定义这些文件夹。  
  
 在没有将 **msdb** 定义为包存储区的一部分的情况下，如果在 **“包路径”** 选项中选择 SQL Server，则可以继续使包与现有逻辑文件夹关联。  
  
> [!NOTE]  
>  在保存包的副本之前，必须在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开包。  
  
### <a name="to-save-a-copy-of-a-package"></a>保存包的副本  
  
1.  在解决方案资源管理器中，双击要保存其副本的包。  
  
2.  在“文件”菜单上，单击“包文件\<的副本 > 另存为”。  
  
3.  在 **“保存包的副本”** 对话框，在 **“包位置”** 列表中选择包的位置。  
  
4.  如果位置为 **SQL Server** 或 **“SSIS 包存储区”**，请提供服务器名称。  
  
5.  如果保存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请指定身份验证类型；如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，还请提供用户名和密码。  
  
6.  若要指定包路径，请键入路径或单击浏览按钮 **(…)** ，以指定包的位置。 包的默认名称为 Package。 也可以将包名称更新为所需的名称。  
  
     如果选择 **SQL Server** 作为 **“包路径”** 选项，则包路径由 **msdb** 中的逻辑文件夹和包名称构成。 例如，如果包 DownloadMonthlyData 与 MSDB 文件夹中的 Finance 文件夹（ **msdb**中的根逻辑文件夹的默认名称）相关联，则名为 DownloadMonthlyData 的包的包路径为 MSDB/Finance/DownloadMonthlyData  
  
     如果选择 **“SSIS 包存储区”** 作为 **“包路径”** 选项，则包路径由 Integration Services 服务管理的文件夹构成。 例如，如果包 UpdateDeductions 位于该服务所管理的文件系统文件夹中的 HumanResources 文件夹内，则包路径为 /File System/HumanResources/UpdateDeductions；同样，如果包 PostResumes 与 MSDB 文件夹中的 HumanResources 文件夹关联，则包路径为 MSDB/HumanResources/PostResumes。  
  
     如果选择 **“文件系统”** 作为 **“包路径”** 选项，则包路径为文件系统中的位置和文件名。 例如，如果包名称为 UpdateDemographics，则包路径为 C:\HumanResources\Quarterly\UpdateDemographics.dtsx。  
  
7.  查看包保护级别。  
  
8.  还可以单击“保护级别”旁边的 **(…)** 浏览按钮，更改保护级别。  
  
    -   在 **“包保护级别”** 对话框中，选择不同的保护级别。  
  
    -   单击“确定” 。  
  
9. 单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;包](../../2014/integration-services/integration-services-ssis-packages.md)   
 [配置 Integration Services 服务&#40;SSIS 服务&#41;](service/integration-services-service-ssis-service.md)  
  
  