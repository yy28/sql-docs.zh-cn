---
title: “更新表”对话框
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 19251316d4674ad7632c6f220f85e2178f4365ca
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004123"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>“更新表”对话框 (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

使用此对话框，可以指定要更新的表。

在您将查询的类型更改为“更新”查询时，如果“关系图”窗格中显示了多个表，则将显示此对话框。  

选择要更新的表，然后选择“确定”  。

> [!NOTE]
> 如果表是为复制发布的，则必须使用 Transact-SQL 语句 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 或 SQL Server 管理对象 (SMO) 对架构进行更改。 使用表设计器或数据库关系图设计器更改架构后，会尝试删除并重新创建表。 由于您不能删除已发布的对象，因此架构更改将失败。

## <a name="see-also"></a>另请参阅

[创建更新查询](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)