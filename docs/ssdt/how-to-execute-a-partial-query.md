---
title: 执行部分查询
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: af04ab37-6cbb-4185-9382-e5922fa5b1df
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 5786127626a655e47e2f6eb4ba96f0a16b740258
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241420"
---
# <a name="how-to-execute-a-partial-query"></a>如何执行部分查询

Transact\-SQL 编辑器允许突出显示特定的脚本段落并将其作为单个查询执行。 这便于您调试复杂查询部分。  
  
> [!WARNING]  
> 以下过程利用在[连接的数据库开发](../ssdt/connected-database-development.md)和[面向项目的脱机数据库开发](../ssdt/project-oriented-offline-database-development.md)部分中的之前过程中创建的实体。  
  
## <a name="to-partially-execute-a-query"></a>部分执行查询  
  
1. 在“SQL Server 对象资源管理器”中，双击“视图”下的 PerishableFruits 以在 Transact\-SQL 编辑器中将其打开。  
  
2. 突出显示代码中的 `SELECT p.Id, p.Name FROM dbo.Product p` 段，右键单击并选择“执行查询”  。  
  
3. 请注意，在 `Products` 表中具有指定字段的所有行都将在“结果”  窗格中返回。