---
title: 保存 SSIS 包（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9f74d9089bf6c2a87edaeaee80c95757982f6c2a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966199"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>保存 SSIS 包（SQL Server 导入和导出向导）
  使用 "**保存 SSIS 包**" 页可以命名、描述 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services （）包并将其保存到数据库中，也可以保存 [!INCLUDE[ssIS](../../includes/ssis-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` 到扩展名为 .dtsx 的文件中。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，未提供用来保存该向导所创建的包的选项。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="static-options"></a>静态选项  
 **名称**  
 为包提供唯一的名称。  
  
 **说明**  
 为包提供说明。 最好按照包的用途对其进行说明，使其一目了然，便于维护。  
  
 **Target**  
 查看以前为目标文件指定的目标对象（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或文件）  
  
## <a name="target-dynamic-options"></a>目标动态选项  
  
### <a name="target--sql-server"></a>目标 = SQL Server  
 **服务器名称**  
 在选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标后，键入或选择目标服务器名称。  
  
 **Use Windows Authentication**  
 在选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标后，指定是否使用 Windows 集成身份验证连接到服务器。 这是首选的身份验证方法。  
  
 **使用 SQL Server 身份验证**  
 在选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标后，指定是否使用 SQL Server 身份验证连接到服务器。  
  
 **用户名**  
 在选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标，并且指定 SQL Server 身份验证后，键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户名。  
  
 **密码**  
 在选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标，并且指定 SQL Server 身份验证后，键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密码。  
  
### <a name="target--file-system"></a>目标 = 文件系统  
 **文件名**  
 选择了文件目标后，请键入目标文件的路径，或使用 "**浏览**" 按钮。  
  
 **浏览**  
 选择文件目标后，使用 "**保存包**" 对话框浏览到目标文件。  
  
## <a name="see-also"></a>另请参阅  
 [保存包](../save-packages.md)  
  
  
