---
title: 检查包含可疑页的数据库的完整性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3b1ec9fe-f6c5-46f7-aa63-6e671be1572d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8abad1f3dbeb8a8667999e90de63d80c2328d90c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866834"
---
# <a name="check-integrity-of-database-with-suspect-pages"></a>检查包含可疑页的数据库的完整性
  此规则检查数据库状态设置为可疑的用户数据库。 当 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 读取包含 824 错误的数据库页时，该页将被视为可疑，其页 ID 将记录在 msdb 的 suspect_pages 表中，并且包含该页的数据库将设置为可疑。  
  
 错误 824 表示在读取操作期间检测到逻辑一致性错误。 此错误通常表示由有问题的 I/O 子系统组件引起的数据损坏。 这是一个威胁数据库完整性的严重错误条件，必须立即纠正。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
  
-   查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以了解此数据库的 824 错误的详细信息。  
  
-   完成完整的数据库一致性检查 ([DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql))。  
  
-   实现在 [MSSQLSERVER_824](https://go.microsoft.com/fwlink/?LinkId=81397)中定义的用户操作。  
  
## <a name="for-more-information"></a>有关详细信息  
 [管理 suspect_pages 表 (SQL Server)](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
