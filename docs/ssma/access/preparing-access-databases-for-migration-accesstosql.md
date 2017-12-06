---
title: "准备迁移 (AccessToSQL) 访问数据库 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "20"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: 7acee61cd57706ff696abda0fae9c48d6bfaaeac
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>准备迁移 (AccessToSQL) 访问数据库
在迁移到 Access 数据库之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，必须确定哪些数据库迁移，并确保这些数据库可供迁移。  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>确定何时迁移到 SQL Server  
Jet 数据库引擎，用于存储作为数据库引擎访问，是用于数据管理的灵活、 更易于使用的解决方案。 但是，作为变得更大的数据库和多个任务关键型，许多用户发现它们需要更高的性能、 安全性或可用性。 对于需要更可靠的数据平台的应用程序，请考虑将移动到这些应用程序的基础数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关确定何时迁移的详细信息，请参阅[迁移信息页](http://go.microsoft.com/fwlink/?LinkId=68571)上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Web 站点。  
  
你将数据库迁移到后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可以继续使用访问通过使用链接的表，或您可以手动迁移您的应用程序[!INCLUDE[msCoName](../../includes/msconame_md.md)]基于.NET Framework 的代码，从而直接与交互[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
## <a name="determining-which-databases-to-migrate"></a>确定哪些数据库迁移  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) 进行访问可以找到用于你的 Access 数据库。 然后可以将导出到这些数据库有关的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关如何导出和查询元数据的详细信息，请参阅[导出访问清单](http://msdn.microsoft.com/7e1941fb-3d14-4265-aff6-c77a4026d0ed)。  

   > [!NOTE]
   > 并非所有访问功能和设置支持，或者可以轻松地转换成[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 在开始迁移数据库之前，请参阅[不兼容的访问功能](http://msdn.microsoft.com/99d45b9c-e3b9-4d56-8c25-b594b887ace1)。
  
## <a name="preparing-for-migration"></a>准备迁移  
使用以下准则来帮助你准备你的 Access 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
### <a name="upgrading-older-access-databases"></a>升级较旧的 Access 数据库  
访问的 SSMA 支持 Access 97 和更高版本。 如果必须从早期版本的 Access 数据库，请打开，并将数据库保存在 Access 97 或更高版本。  
  
### <a name="removing-workgroup-protection"></a>删除工作组保护  
SSMA 无法迁移使用工作组保护的数据库。 若要从 Access 数据库中删除工作组保护，请执行以下步骤：  
  
1.  将 Access 数据库文件复制到另一个位置。  
  
2.  打开复制的数据库。  
  
3.  上**工具**菜单上，指向**安全**，然后选择**用户和组权限**。  
  
4.  选择**用户**选项中，选择**管理员**用户，然后确保**管理**权限已被选中。  
  
5.  选择**组**选项中，选择**用户**组，然后确保**管理**权限已被选中。  
  
6.  单击**确定**，然后在**文件**菜单上，单击**退出**。  
  
你现在可以使用 SSMA 迁移复制的数据库。 加载到架构后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你可以手动保护数据库的安全上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
### <a name="backing-up-databases"></a>备份数据库  
在迁移到 Access 数据库之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你应当备份计算机上你将迁移的这两个访问数据库以及[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]要迁移到其中的数据库访问对象和数据。  
  
若要备份上的 Access 数据库中，**工具**菜单上，指向**数据库实用程序**，然后选择**备份数据库**。  
  
有关如何备份[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库，请参阅"Backing Up and Restoring Databases 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
### <a name="documenting-databases"></a>记录数据库  
您可能还要向文档属性，如数据库对象、 文件大小、 和权限，你的 Access 数据库的列表。 若要在生成在 Access 中，此文档**工具**菜单上，指向**分析**，然后单击**记录**。  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[链接到 SQL Server 访问应用程序](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)
