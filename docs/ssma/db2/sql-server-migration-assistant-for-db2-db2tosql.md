---
title: DB2 (DB2ToSQL) 的 SQL Server 迁移助手 |Microsoft Docs
description: 了解 SSMA for DB2 并按照逐步说明将 DB2 数据库迁移到 SQL Server 或 Azure SQL 数据库。
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7633f631-ffad-469a-8441-8831a6a9f932
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 6ade3ce31bed08bdb7b25b09ec0d5bbcf91405f1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936476"
---
# <a name="sql-server-migration-assistant-for-db2-db2tosql"></a>DB2 (DB2ToSQL) 的 SQL Server 迁移助手
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Db2 的迁移助手 (SSMA) 是将 db2 数据库迁移到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的工具[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 和 linux 上的2012、2014、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017、windows 和 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] linux 上的2019或 Azure SQL 数据库。 SSMA for DB2 将 DB2 数据库对象转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象，在中创建这些对象， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 然后将数据从 DB2 迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL 数据库。  
  
本文档介绍 SSMA for DB2，并提供有关将 DB2 数据库迁移到的分步说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 下表显示了可帮助你了解更多详细信息的文章：  
  
## <a name="contents"></a>目录  
  
|部分|说明|  
|-----------|---------------|
|[SSMA for DB2 中的新增功能](https://msdn.microsoft.com/1cc38f85-3caa-42d0-8c76-a380c1d15c67)|此版本的 SSMA for DB2 中的新增功能|  
|[安装 SSMA for DB2 Client &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)|包含一些文章，这些文章提供了在运行的计算机上为 DB2 客户端和所需组件安装 SSMA 的先决条件和说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|[SSMA for DB2 &#40;DB2ToSQL&#41;的入门](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)|介绍用户界面、项目和配置选项。|  
|[将 DB2 数据库迁移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)|概述转换过程，并提供有关过程中每个步骤的详细信息。|  
|[用户界面参考 &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)|包含用于 DB2 对话框的 SSMA 文档。|  
|[使用 SSMA for DB2 控制台](https://msdn.microsoft.com/29d8787c-632e-4ff7-9ccc-3f7ad40480ec)|包含有关 SSMA 控制台应用程序的文档|  
|[获取用于 DB2 帮助的 SSMA](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有关获取其他帮助的信息。|  
