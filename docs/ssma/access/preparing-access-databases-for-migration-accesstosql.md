---
title: 准备访问数据库以进行迁移 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 9495ff7a58da124255cc6bf5674d92ebeef4c2b0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677666"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>准备迁移 (AccessToSQL) 访问数据库
在迁移到 Access 数据库之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，必须确定哪些数据库迁移，并确保这些数据库已准备好进行迁移。  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>确定何时将迁移到 SQL Server  
Jet 数据库引擎，用于为数据库引擎访问，是一个灵活、 易于使用解决方案，数据管理。 但是，作为变得更大的数据库和多个关键任务应用程序，许多用户发现，它们需要更高的性能、 安全性或可用性。 对于需要更可靠的数据平台的应用程序，请考虑将移到这些应用程序的基础数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 确定何时要迁移的详细信息，请参阅[迁移信息页](https://go.microsoft.com/fwlink/?LinkId=68571)上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Web 站点。  
  
迁移到数据库后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以继续通过使用链接的表，使用访问权限或可以手动迁移到应用程序[!INCLUDE[msCoName](../../includes/msconame_md.md)]直接交互的基于.NET Framework 的代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="determining-which-databases-to-migrate"></a>确定要迁移的数据库  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 迁移助手 (SSMA) for Access 可以为你找到访问数据库。 然后，可以导出到这些数据库有关的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关如何导出和查询的元数据的详细信息，请参阅[导出 Access 清单](exporting-an-access-inventory-accesstosql.md)。  

   > [!NOTE]
   > 并非所有访问功能和设置支持，或者可以轻松地转换成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在开始迁移数据库之前，请参阅[不兼容的访问功能](incompatible-access-features-accesstosql.md)。
  
## <a name="preparing-for-migration"></a>准备迁移  
使用以下准则来帮助准备您的 Access 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
### <a name="upgrading-older-access-databases"></a>升级较旧的 Access 数据库  
适用于 Access 的 SSMA 支持 Access 97 和更高版本。 如果是从早期版本的访问权限的数据库，打开并保存在 Access 97 或更高版本中的数据库。  
  
### <a name="removing-workgroup-protection"></a>删除工作组保护  
SSMA 无法迁移使用工作组保护的数据库。 若要从 Access 数据库中删除工作组保护，请执行以下步骤：  
  
1.  将 Access 数据库文件复制到另一个位置。  
  
2.  打开复制的数据库。  
  
3.  上**工具**菜单，依次指向**安全**，然后选择**用户和组权限**。  
  
4.  选择**用户**选项，选中**管理员**用户，然后确保**管理**权限已被选中。  
  
5.  选择**组**选项，选中**用户**组，然后确保**管理**权限已被选中。  
  
6.  单击**确定**，然后在**文件**菜单中，单击**退出**。  
  
现在可以使用 SSMA 将复制的数据库迁移。 加载架构读入后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以手动上保护数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
### <a name="backing-up-databases"></a>备份数据库  
在迁移到您的 Access 数据库之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，应备份将迁移这两个访问数据库并将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将迁移到其中的数据库访问对象和数据。  
  
若要备份上的 Access 数据库中，**工具**菜单，依次指向**数据库实用程序**，然后选择**备份数据库**。  
  
有关如何备份[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，请参阅"备份和还原数据库中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
### <a name="documenting-databases"></a>记录数据库  
您可能想要记录的属性，例如的数据库对象、 文件大小和权限，您的 Access 数据库的列表。 若要在生成在 Access 中，此文档**工具**菜单，依次指向**分析**，然后单击**文档化**。  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[链接到 SQL Server 访问应用程序](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
