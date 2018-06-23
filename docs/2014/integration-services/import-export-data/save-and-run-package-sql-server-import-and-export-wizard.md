---
title: 保存并执行包 （SQL Server 导入和导出向导） |Microsoft 文档
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6071acee5eb7d888bdf4182a30f433e531754f64
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027023"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>保存并执行包（SQL Server 导入和导出向导）
  使用**保存和执行包**对话框中，保存它以便以后运行，和 / 或立即运行包。  
  
> [!NOTE]  
>  如果你停止它之前的包完成运行，不保存包，即使你选择**保存**复选框。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解有关启动向导，以及成功运行向导所需的权限的选项，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>“常规”  
 **立即执行**  
 选择此选项将立即运行包。  
  
 **保存 SSIS 包**  
 保存包以便日后运行，也可以根据需要立即运行包。  
  
> [!NOTE]  
>  在[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，以保存由向导创建的包的选项不可用。  
  
 **SQL Server**  
 选择此选项可保存到包[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb`数据库。  
  
> [!NOTE]  
>  仅当选择了此选项才可用**保存 SSIS 包**选项。  
  
 **文件系统**  
 选择此选项可以将包保存为扩展名为 .dtsx 的文件。  
  
> [!NOTE]  
>  仅当选择了此选项才可用**保存 SSIS 包**选项。  
  
 **包保护级别**  
 从列表中选择保护级别。  
  
 保护级别决定保护包时所使用的方法、密码或用户密钥以及作用域。 可以保护所有数据，也可以只保护敏感数据。 若要了解要求和有关包安全的选项，请参阅[Access Control for Sensitive Data in Packages](../security/access-control-for-sensitive-data-in-packages.md)和[安全概述&#40;Integration Services&#41;](../security/security-overview-integration-services.md)。  
  
> [!NOTE]  
>  仅当选择了此选项才可用**保存 SSIS 包**选项。  
  
 **密码**  
 键入密码。  
  
> [!NOTE]  
>  仅当已设置此选项才可用**包保护级别**选项为**使用密码加密敏感数据**或**使用密码加密所有数据**。  
  
 **重新键入密码**  
 再次键入该密码。  
  
> [!NOTE]  
>  仅当已设置此选项才可用**包保护级别**选项为**使用密码加密敏感数据**或**使用密码加密所有数据**。  
  
## <a name="see-also"></a>请参阅  
 [项目和包的执行](../packages/run-integration-services-ssis-packages.md)   
 [保存包](../save-packages.md)  
  
  