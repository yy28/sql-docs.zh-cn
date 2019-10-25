---
title: 多次大容量复制操作
description: 介绍如何使用 SqlBulkCopy 类在 SQL Server 的实例中执行多个大容量复制操作。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5ad12f94-7459-4a93-a421-4160d1a90715
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 6cc373224f4df437665cc48edb78ff81b85b8ac1
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452130"
---
# <a name="multiple-bulk-copy-operations"></a>多次大容量复制操作

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

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
