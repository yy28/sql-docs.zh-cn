---
title: 包备份和还原（SSIS 服务） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, backup and restore
- backing up packages [Integration Services]
- packages [Integration Services], backup and restore
- SQL Server Integration Services packages, backup and restore
- restoring packages [Integration Services]
- Integration Services packages, backup and restore
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5c775393f7815084e8a79aae4be7f0974886f3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056924"
---
# <a name="package-backup-and-restore-ssis-service"></a>包备份和还原（SSIS 服务）
    
> [!IMPORTANT]  
>  本主题论述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]支持服务以便与的早期版本向后兼容[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]可以将包保存到文件系统或 msdb （一种[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]系统数据库）中。 可以使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份和还原功能来备份和还原保存到 msdb 中的包。  
  
 有关备份和还原 msdb 数据库的详细信息，请单击下列某个主题：  
  
-   [SQL Server 数据库的备份和还原](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [备份和还原系统数据库 (SQL Server)](../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]包括可用于管理包的**dtutil**命令提示实用工具（dtutil）。 有关详细信息，请参阅 [dtutil Utility](dtutil-utility.md)。  
  
## <a name="configuration-files"></a>配置文件  
 包所包括的所有配置文件都存储在文件系统中。 在备份 msdb 数据库时并不会备份这些文件；因此，你应该确保定期备份配置文件，以便保护保存到 msdb 中的包。 若要将配置包括在 msdb 数据库的备份中，应该考虑使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置类型，而不使用基于文件的配置。  
  
## <a name="packages-stored-in-the-file-system"></a>在文件系统中存储的包  
 备份服务器文件系统的计划中应当包括对保存到文件系统的包的备份。 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务配置文件的默认名称为 MsDtsSrvr.ini.xml，它列出服务器上该服务所监视的文件夹。 您应该确保备份这些文件夹。 另外，包可以存储在服务器上的其他文件夹中，因此应该确保在备份中包括这些文件夹。  
  
  
