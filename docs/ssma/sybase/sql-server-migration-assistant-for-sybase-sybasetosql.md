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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72252152"
---
# <a name="sql-server-migration-assistant-for-sybase-sybasetosql"></a>Sybase 的 SQL Server 迁移助手（SybaseToSQL）

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于 Sybase 自适应服务器企业（ASE）的迁移助手（SSMA）是一种用于将 ASE [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库迁移[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到 2012 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2014 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2016、2017 on windows [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 linux、windows 和 linux 上[!INCLUDE[msCoName](../../includes/msconame_md.md)]的2019或 Azure SQL 数据库的工具。 SSMA for Sybase 将 ASE 数据库对象转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为数据库对象，在或 Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sql 数据库中创建这些对象，然后将数据从 ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]迁移到或 azure sql 数据库。
  
本文档介绍了如何为 Sybase SSMA，并提供了将 ASE 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 数据库的分步说明，并提供了迁移后可能出现的问题的相关信息。 若要了解详细信息，请参阅以下文章。  
  
## <a name="contents"></a>目录  
  
|节|说明|
|-----------|---------------|
|[Sybase &#40;SybaseToSQL 的 SSMA 中的新增功能&#41;](../../ssma/sybase/what-s-new-in-ssma-for-sybase-sybasetosql.md)|列出对 SSMA 版本的更改。|  
|[为 Sybase &#40;SybaseToSQL&#41;安装 SSMA](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)|包含一些文章，这些文章提供了在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的计算机上为 Sybase 客户端和所需组件安装 SSMA 的先决条件和说明。|  
|[入门用于 Sybase &#40;SybaseToSQL 的 SSMA&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)|介绍用户界面、项目和配置选项。|  
|[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)|概述转换过程，并提供有关过程中每个步骤的详细信息。|  
|[用户界面参考 &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)|包含用于 Sybase 对话框的 SSMA 文档。|  
|[使用 SSMA for Sybase 控制台](working-with-ssma-for-sybase-console-sybasetosql.md)|包含有关 SSMA 控制台应用程序的文档。|  
|[获取用于 Sybase 帮助的 SSMA](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有关获取其他帮助的信息。|  
