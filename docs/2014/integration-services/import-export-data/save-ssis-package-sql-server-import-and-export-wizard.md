---
title: 保存 SSIS 包（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b8ef62839d7379c35b55af7bcb65ab46e4b455d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048228"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>保存 SSIS 包（SQL Server 导入和导出向导）
  使用**保存 SSIS 包**页可以命名、 描述和保存[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 打包到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`msdb`数据库或具有.dtsx 到文件扩展插件。  
  
> [!NOTE]  
>  在[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，用于保存由向导创建的包的选项不可用。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解有关用于启动向导，选项以及已成功运行该向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="static-options"></a>静态选项  
 **名称**  
 为包提供唯一的名称。  
  
 **描述**  
 为包提供说明。 最好按照包的用途对其进行说明，使其一目了然，便于维护。  
  
 **Target**  
 查看目标 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或文件) 的以前指定的目标文件。  
  
## <a name="target-dynamic-options"></a>目标动态选项  
  
### <a name="target--sql-server"></a>目标 = SQL Server  
 **服务器名称**  
 在选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标后，键入或选择目标服务器名称。  
  
 **Use Windows Authentication**  
 在选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标后，指定是否使用 Windows 集成身份验证连接到服务器。 这是首选的身份验证方法。  
  
 **Use SQL Server Authentication**  
 在选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标，指定是否使用 SQL Server 身份验证连接到服务器。  
  
 **用户名**  
 在选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标，并指定了 SQL Server 身份验证，键入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户名称。  
  
 **密码**  
 在选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标，并指定了 SQL Server 身份验证，键入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]密码。  
  
### <a name="target--file-system"></a>目标 = 文件系统  
 **文件名**  
 当选择了文件目标后时，键入目标文件的路径，或使用**浏览**按钮。  
  
 **“浏览”**  
 当你选择了文件目标时，通过浏览到目标文件**保存包**对话框。  
  
## <a name="see-also"></a>请参阅  
 [保存包](../save-packages.md)  
  
  
