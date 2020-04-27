---
title: 保存并执行包（SQL Server 导入和导出向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 517ba30e4565ec05e5fa15a650bb39909d24dd02
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62894761"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>保存并执行包（SQL Server 导入和导出向导）
  使用 "**保存并执行包**" 对话框可以立即运行包，将其保存到稍后运行。  
  
> [!NOTE]  
>   如果在包完成运行前停止包，即使选中了 **“保存”** 复选框，也不会保存该包。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解用于启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **立即执行**  
 选择此选项将立即运行包。  
  
 **保存 SSIS 包**  
 保存包以便日后运行，也可以根据需要立即运行包。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中，未提供用来保存该向导所创建的包的选项。  
  
 **SQL Server**  
 选择此选项可将包保存到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb`数据库。  
  
> [!NOTE]  
>  仅当选择了 "**保存 SSIS 包**" 选项时，此选项才可用。  
  
 **文件系统**  
 选择此选项可以将包保存为扩展名为 .dtsx 的文件。  
  
> [!NOTE]  
>  仅当选择了 "**保存 SSIS 包**" 选项时，此选项才可用。  
  
 **“包保护级别”**  
 从列表中选择保护级别。  
  
 保护级别决定保护包时所使用的方法、密码或用户密钥以及作用域。 可以保护所有数据，也可以只保护敏感数据。 若要了解包安全性的要求和选项，请参阅[对包中敏感数据的访问控制](../security/access-control-for-sensitive-data-in-packages.md)和[安全概述 &#40;Integration Services&#41;](../security/security-overview-integration-services.md)。  
  
> [!NOTE]  
>  仅当选择了 "**保存 SSIS 包**" 选项时，此选项才可用。  
  
 **密码**  
 键入密码。  
  
> [!NOTE]  
>  仅当已将 "**包保护级别**" 选项设置为 "**使用密码加密敏感数据**" 或 "**使用密码加密所有数据**" 时，此选项才可用。  
  
 **重新键入密码**  
 再次键入该密码。  
  
> [!NOTE]  
>  仅当已将 "**包保护级别**" 选项设置为 "**使用密码加密敏感数据**" 或 "**使用密码加密所有数据**" 时，此选项才可用。  
  
## <a name="see-also"></a>另请参阅  
 [项目和包的执行](../packages/run-integration-services-ssis-packages.md)   
 [保存包](../save-packages.md)  
  
  
