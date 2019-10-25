---
title: SQL XML 列值
description: 演示如何检索和使用从 SQL Server 检索的 XML 数据。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8dc9d5100f71fed39c1e4166882230451dd139e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451938"
---
# <a name="sql-xml-column-values"></a>SQL XML 列值

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 支持 `xml` 数据类型，开发人员可以使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 类的标准行为检索包括此类型的结果集。 可以像检索任何列一样检索 `xml` 列 <xref:Microsoft.Data.SqlClient.SqlDataReader> （例如），但如果想要以 XML 形式处理列的内容，则必须使用 <xref:System.Xml.XmlReader>。  
  
## <a name="example"></a>示例  
以下控制台应用程序从 AdventureWorks 数据库的 Sales.Store 表中为 <xref:Microsoft.Data.SqlClient.SqlDataReader> 实例选择两行，每行包含一个 `xml` 列。 对于每一行，`xml` 列的值是使用 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 方法读取的。 值存储在 <xref:System.Xml.XmlReader> 中。 请注意，如果要将内容设置为 <xref:System.Data.SqlTypes.SqlXml> 变量，则必须使用 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 而不是 <xref:System.Data.IDataRecord.GetValue%2A> 方法; <xref:System.Data.IDataRecord.GetValue%2A> 将 `xml` 列的值作为字符串返回。  
  
> [!NOTE]
>  默认情况下，在安装 SQL Server 时不安装 AdventureWorks 示例数据库。 可以通过运行 SQL Server 安装程序来安装它。  
  
[!code-csharp[DataWorks SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>后续步骤
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server 中的 XML 数据](xml-data-sql-server.md)
