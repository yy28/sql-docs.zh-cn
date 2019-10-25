---
title: SQL Server 数据类型和 ADO.NET
description: 介绍如何使用 SQL Server 数据类型，以及它们如何与 .NET 数据类型交互。
ms.date: 08/15/2019
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 12ad13d6788ae2b8995289100883b06c5ab6d7c6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452033"
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server 数据类型和 ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 和 .NET 基于不同类型系统，这可能会导致潜在的数据丢失。 为了保持数据完整性，适用于 SQL Server 的 Microsoft SqlClient 数据提供程序（<xref:Microsoft.Data.SqlClient>）提供了用于处理 SQL Server 数据的类型化访问器方法。 您可以使用 <xref:System.Data.SqlDbType> 类中的枚举来指定 <xref:Microsoft.Data.SqlClient.SqlParameter> 数据类型。  
  
SQL Server 2008 引入了新的数据类型，这些数据类型旨在满足企业使用日期和时间、结构化、半结构化和非结构化数据的需要。 相关文档位于 SQL Server 2008 联机丛书中。  
  
可在应用程序中使用 SQL Server 数据类型取决于所使用 SQL Server 的版本。 有关详细信息，请参阅 SQL Server 联机丛书中的[数据类型（数据库引擎）](https://go.microsoft.com/fwlink/?LinkID=107468) 。
  
## <a name="in-this-section"></a>在本节中  
[SqlTypes 和 DataSet](sqltypes-dataset.md)  
介绍对 `DataSet` 中 `SqlTypes` 的类型支持。  
  
[处理 null 值](handle-null-values.md)  
演示如何处理 null 值和三值逻辑。  
  
[比较 GUID 和 uniqueidentifier 值](compare-guid-uniqueidentifier-values.md)  
演示如何在 SQL Server 和 .NET 中使用 GUID 和 uniqueidentifier 值。  
  
[日期和时间数据](date-time-data.md)  
介绍如何使用 SQL Server 2008 中引入的新日期和时间数据类型。  
  
[大型 UDT](large-udts.md)  
演示如何从 SQL Server 2008 中引入的大值 Udt 检索数据。  
  
[SQL Server 中的 XML 数据](xml-data-sql-server.md)  
介绍如何使用从 SQL Server 检索的 XML 数据。  
  
## <a name="reference"></a>参考  
<xref:System.Data.DataSet>  
描述 `DataSet` 类及其所有成员。  
  
<xref:System.Data.SqlTypes>  
介绍 `SqlTypes` 命名空间及其所有成员。  
  
<xref:System.Data.SqlDbType>  
描述 `SqlDbType` 枚举及其所有成员。  
  
<xref:System.Data.DbType>  
描述 `DbType` 枚举及其所有成员。  
  
## <a name="next-steps"></a>后续步骤
- [表值参数](table-valued-parameters.md)
- [SQL Server 二进制和大值数据](sql-server-binary-large-value-data.md)
