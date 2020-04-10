---
title: SQL Server 二进制和大值数据
description: 介绍如何在 SQL Server 中使用大值数据。
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 17a38bd45a467625be467f5fb01f0e733f7546bc
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920974"
---
# <a name="sql-server-binary-and-large-value-data"></a>SQL Server 二进制和大值数据

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 提供了 `max` 说明符以扩展 `varchar`、`nvarchar` 和 `varbinary` 数据类型的存储容量。 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)` 统称为“大值数据类型”  。 你可以使用大值数据类型来存储长达 2^31-1 个字节的数据。  
  
SQL Server 2008 引入了 FILESTREAM 属性，该属性不是数据类型，而是可以在列上定义的属性，从而允许大值数据存储在文件系统而不是数据库中。  
  
## <a name="in-this-section"></a>在本节中  
[修改 ADO.NET 中的大值（最大值）数据](modify-large-value-max-data.md)  
说明如何使用大值数据类型。  
  
[FILESTREAM 数据](filestream-data.md)  
介绍如何使用 FILESTREAM 属性处理 SQL Server 2008 中存储的大值数据。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 数据类型和 ADO.NET](sql-server-data-types.md)
- [ADO.NET 中的 SQL Server 数据操作](sql-server-data-operations.md)
