---
title: SqlTypes 和数据集
description: 介绍数据集中 SqlTypes 的类型支持。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 2d6f5ec17e800cbac571554a359c2ebd43fa9186
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918577"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes 和数据集

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

ADO.NET 2.0 通过 `DataSet` 命名空间引入了对 <xref:System.Data.SqlTypes> 的增强类型支持。 <xref:System.Data.SqlTypes> 中的类型旨在提供具有与 SQL Server 数据库中的数据类型相同的语义和精度的数据类型。 <xref:System.Data.SqlTypes> 中的每个数据类型在 SQL Server 中都具有等效的数据类型，并具有相同的基础数据表示形式。  
  
使用 SQL Server 数据类型时，直接在 <xref:System.Data.SqlTypes> 中使用 <xref:System.Data.DataSet> 将带来许多好处。 <xref:System.Data.SqlTypes> 支持与 SQL Server 本机数据类型相同的语义。 在 <xref:System.Data.SqlTypes> 的定义中指定其中一个 <xref:System.Data.DataColumn> 将消除将十进制或数值数据类型转换为公共语言运行时 (CLR) 数据类型之一时可能出现的精度损失。  

以下代码创建 <xref:System.Data.DataTable> 对象，使用 <xref:System.Data.DataColumn>（而不是 CLR 类型）显式定义 <xref:System.Data.SqlTypes> 数据类型。 代码用 SQL Server 中 AdventureWorks 数据库的 Sales.SalesOrderDetail 表中的数据填充 <xref:System.Data.DataTable>。 控制台窗口中显示的输出显示每个列的数据类型以及从 SQL Server 检索的值。  
  
[!code-csharp[DataWorks DataColumn_DataType#1](~/../sqlclient/doc/samples/DataColumn_DataType.cs#1)]
