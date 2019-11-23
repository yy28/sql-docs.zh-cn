---
title: Sybase 的 SQL Server 迁移助手（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59e63eac-8a7e-4d54-be1c-0633a9bf510d
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 3913ae22155ca5e560db7fee946df0f8062a23b9
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252152"
---
# <a name="sql-server-migration-assistant-for-sybase-sybasetosql"></a>Sybase 的 SQL Server 迁移助手（SybaseToSQL）

Sybase 自适应服务器 Enterprise （ASE）的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 迁移助手（SSMA）是一种工具，用于将 ASE 数据库迁移到 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012，[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014，[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016，在 Windows 和 linux 上 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 2019，或 [!INCLUDE[msCoName](../../includes/msconame_md.md)]Azure SQL 数据库。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[msCoName](../../includes/msconame_md.md)] SSMA for Sybase 将 ASE 数据库对象转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL 数据库中创建这些对象，然后将数据从 ASE 迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL 数据库。
  
本文档介绍 SSMA for Sybase，并提供将 ASE 数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL 数据库的分步说明，并提供迁移后可能出现的问题的相关信息。 若要了解详细信息，请参阅以下文章。  
  
## <a name="contents"></a>内容  
  
|部分|描述|
|-----------|---------------|
|[Sybase &#40;SYBASETOSQL 中 SSMA 的新增功能&#41;](../../ssma/sybase/what-s-new-in-ssma-for-sybase-sybasetosql.md)|列出对 SSMA 版本的更改。|  
|[为 Sybase &#40;SYBASETOSQL 安装 SSMA&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)|包含一些文章，这些文章提供了在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机上为 Sybase 客户端和所需组件安装 SSMA 的先决条件和说明。|  
|[入门用于 Sybase &#40;SYBASETOSQL 的 SSMA&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)|介绍用户界面、项目和配置选项。|  
|[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL &#40;DB SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)|概述转换过程，并提供有关过程中每个步骤的详细信息。|  
|[用户界面参考&#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)|包含用于 Sybase 对话框的 SSMA 文档。|  
|[使用 SSMA for Sybase 控制台](working-with-ssma-for-sybase-console-sybasetosql.md)|包含有关 SSMA 控制台应用程序的文档。|  
|[获取用于 Sybase 帮助的 SSMA](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有关获取其他帮助的信息。|  
