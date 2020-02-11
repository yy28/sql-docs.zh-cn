---
title: DB2 的 SQL Server 迁移助手（DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7633f631-ffad-469a-8441-8831a6a9f932
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 62b4910d6073da7ec845cc5e754a4e005f5d1461
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "72252163"
---
# <a name="sql-server-migration-assistant-for-db2-db2tosql"></a>DB2 的 SQL Server 迁移助手（DB2ToSQL）
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Db2 的迁移助手（SSMA）是一种用于将 db2 数据库迁移[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到 2012 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2014 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2016 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2017 on windows 和 linux [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、windows 和 linux 上的2019或 Azure SQL 数据库的工具。 SSMA for DB2 将 DB2 数据库对象转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为数据库对象，在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建这些对象，然后将数据从 DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]迁移到或 Azure SQL 数据库。  
  
本文档介绍 SSMA for DB2，并提供有关将 DB2 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的分步说明。 下表显示了可帮助你了解更多详细信息的文章：  
  
## <a name="contents"></a>目录  
  
|部分|说明|  
|-----------|---------------|
|[SSMA for DB2 中的新增功能](https://msdn.microsoft.com/1cc38f85-3caa-42d0-8c76-a380c1d15c67)|此版本的 SSMA for DB2 中的新增功能|  
|[安装 SSMA for DB2 Client &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)|包含一些文章，这些文章提供了在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的计算机上为 DB2 客户端和所需组件安装 SSMA 的先决条件和说明。|  
|[SSMA for DB2 &#40;DB2ToSQL&#41;的入门](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)|介绍用户界面、项目和配置选项。|  
|[将 DB2 数据库迁移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)|概述转换过程，并提供有关过程中每个步骤的详细信息。|  
|[用户界面参考 &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)|包含用于 DB2 对话框的 SSMA 文档。|  
|[使用 SSMA for DB2 控制台](https://msdn.microsoft.com/29d8787c-632e-4ff7-9ccc-3f7ad40480ec)|包含有关 SSMA 控制台应用程序的文档|  
|[获取用于 DB2 帮助的 SSMA](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有关获取其他帮助的信息。|  
