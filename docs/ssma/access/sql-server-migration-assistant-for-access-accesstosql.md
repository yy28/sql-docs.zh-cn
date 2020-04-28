---
title: SQL Server 迁移助手访问权限（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: dfa640787f42d06ed65b713c9fea415dc9560a2e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72252210"
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>SQL Server 迁移助手访问权限（AccessToSQL）

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于访问的迁移助手（SSMA）是一种用于将数据库[!INCLUDE[msCoName](../../includes/msconame_md.md)]从 Access 版本 2010 97 到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017、windows 和 linux、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 和 linux 上的2019或[!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL 数据库的迁移工具。 SSMA for Access 将 Access 数据库对象转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为或 azure sql 数据库对象，将这些对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]加载到或 azure sql 数据库，然后将数据从 Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 azure sql 数据库迁移到 azure sql database。
  
本文档介绍如何 SSMA 访问，并提供有关将 Access 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 数据库的分步说明，并提供迁移后可能出现的问题的相关信息。  
  
## <a name="contents"></a>目录  
  
|节|说明|
|-----------|---------------|
|[SSMA for Access 中的新增功能](https://msdn.microsoft.com/a24d3fc0-6911-4bfa-828a-197abf222e02)|列出对 SSMA 版本的更改。|  
|[安装访问 SQL Server 迁移助手](installing-sql-server-migration-assistant-for-access-accesstosql.md)|列出了安装 SSMA 的先决条件、安装和许可 SSMA 的过程，以及指向最新版本的链接。|  
|[使用 SQL Server 迁移助手入门访问 &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|介绍 SSMA 及其用户界面。|  
|[准备要迁移的 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)|描述如何准备要转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 的 Access 数据库。|  
|[将 Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)|概述转换过程，并提供有关过程中每个步骤的详细信息。|  
|[将访问应用程序链接到 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)|描述如何将现有的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access 应用程序用于。|  
|[用户界面参考](user-interface-reference-accesstosql.md)|包含 SSMA 对话框的文档。|  
|[使用 SSMA for Access 控制台](working-with-ssma-for-access-console-accesstosql.md)|包含有关 SSMA 控制台应用程序的文档|  
|[获取访问的 SSMA 帮助](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有关获取其他帮助的信息。|  
