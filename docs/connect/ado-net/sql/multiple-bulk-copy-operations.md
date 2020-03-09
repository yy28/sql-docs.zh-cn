---
title: 多次大容量复制操作
description: 介绍了如何使用 SqlBulkCopy 类多次执行大容量复制操作将数据复制到 SQL Server 实例中。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5ad12f94-7459-4a93-a421-4160d1a90715
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: f052e70d55a789eab731f94ae086d2f47384593c
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896583"
---
# <a name="multiple-bulk-copy-operations"></a>多次大容量复制操作

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

可以使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 类的单个实例执行多次大容量复制操作。 如果复制之间的操作参数已更改（例如，目标表的名称），必须首先更新它们，之后再对任何 WriteToServer 方法进行任何后续调用，如以下示例所示  。 除非已明确更改，否则将所有属性值保持为与给定实例的较早大容量复制上的属性值相同。  
  
> [!NOTE]
>  与每个操作使用单独实例相比，使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 的同一实例执行多次大容量复制操作通常效率更高。  
  
在使用同一 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 对象执行多次大容量复制操作时，对于每个操作中的源信息或目标信息相同与否没有限制。 但是，必须确保每次写入服务器时正确设置列关联信息。  

## <a name="example"></a>示例

> [!IMPORTANT]
>  除非已按[大容量复制示例设置](bulk-copy-example-setup.md)中所述创建了工作表，否则此示例将不会运行。 提供此代码是为了演示仅使用 SqlBulkCopy 时的语法  。 如果源表和目标表位于同一 SQL Server 实例中，可以更便捷地使用 Transact-SQL `INSERT … SELECT` 语句复制数据。  
  
[!code-csharp[DataWorks SqlBulkCopy_._ColumnMappingOrdersDetails#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnMappingOrdersDetails.cs#1)]
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 中的大容量复制操作](bulk-copy-operations-sql-server.md)
