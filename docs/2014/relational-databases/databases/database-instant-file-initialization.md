---
title: 数据库实例文件初始化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initializations [SQL Server]
- fast file initialization (SQL Server)
- file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
ms.openlocfilehash: dedd2c5b8d075dee8aeeb438904137558c664d95
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970207"
---
# <a name="database-instant-file-initialization"></a>数据库实例文件初始化
  初始化数据和日志文件以覆盖之前删除的文件遗留在磁盘上的任何现有数据。 执行以下其中一项操作时，应首先通过用零填充数据和日志文件来初始化这些文件：  
  
-   创建数据库。  
  
-   向现有数据库中添加文件、日志或数据。  
  
-   增大现有文件的大小（包括自动增长操作）。  
  
-   还原数据库或文件组。  
  
 文件初始化会导致这些操作花费更多时间。 但是，首次将数据写入文件后，操作系统就不必用零来填充文件。  
  
## <a name="instant-file-initialization"></a>即时文件初始化  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，可以在瞬间对数据文件进行初始化。 这样可以快速执行上述文件操作。 即时文件初始化功能将回收使用的磁盘空间，而无需使用零填充空间。 相反，新数据写入文件时会覆盖磁盘内容。 日志文件不能立即初始化。  
  
> [!NOTE]  
>  只有在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] 或 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 或更高版本中才可以使用即时文件初始化功能。  
  
 即时文件初始化功能仅在向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 服务帐户授予了 SE_MANAGE_VOLUME_NAME 之后才可用。 Windows Administrator 组的成员拥有此权限，并可以通过将其他用户添加到 **执行卷维护任务** 安全策略中来为其授予此权限。 有关分配用户权限的详细信息，请参阅 Windows 文档。  
  
 当启用 TDE 时，即时文件初始化功能不可用。  
  
 要向一个帐户授予 `Perform volume maintenance tasks` 权限：  
  
1.  在将要创建备份文件的计算机上打开 `Local Security Policy` 应用程序 (`secpol.msc`)。  
  
2.  在左侧窗格中，展开“本地策略” ****，然后单击“用户权限指派” ****。  
  
3.  在右侧窗格中，双击“执行卷维护任务”****。  
  
4.  单击“添加用户或组” **** ，添加用于备份的任何用户帐户。  
  
5.  单击 "**应用**"，然后关闭所有 `Local Security Policy` 对话框。  
  
### <a name="security-considerations"></a>安全注意事项  
 因为只有在新数据写入文件中时才覆盖删除的磁盘内容，因此，未授权的主体可能会访问删除的内容。 当数据库文件连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例之后，可以通过文件中的随机访问控制列表 (DACL) 来降低此信息泄露的风险。 此 DACL 仅允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户和本地管理员访问文件。 但是，当文件分离以后，可以由不具有 SE_MANAGE_VOLUME_NAME 的用户或服务访问。 在备份数据库时，也存在类似风险。 如果未使用适当的 DACL 对备份文件进行保护，则未授权的用户或服务将可以使用删除的内容。  
  
 如果担心可能会泄漏删除的内容，则应执行以下两种或其中一种操作：  
  
-   请始终确保所有分离的数据文件和备份文件都具有限制性的 DACL。  
  
-   通过从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户中撤消 SE_MANAGE_VOLUME_NAME 来禁用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的即时文件初始化功能。  
  
> [!NOTE]  
>  禁用即时文件初始化功能只会影响在用户权限撤消之后创建的文件或其大小增大的文件。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
