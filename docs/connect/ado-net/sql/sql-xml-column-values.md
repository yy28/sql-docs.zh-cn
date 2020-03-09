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
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 4fd63ceb329fd6e6f7768425a1ccf43afa27dd21
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896256"
---
# <a name="sql-xml-column-values"></a>SQL XML 列值

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 支持 `xml` 数据类型，开发人员可以使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 类的标准行为检索包括此类型的结果集。 可以检索 `xml` 列（例如，检索到 <xref:Microsoft.Data.SqlClient.SqlDataReader> 中），就像检索任何列一样；但若要以 XML 格式处理列内容，必须使用 <xref:System.Xml.XmlReader>。  
  
## <a name="example"></a>示例  
以下控制台应用程序从 AdventureWorks 数据库的 Sales.Store 表中为 <xref:Microsoft.Data.SqlClient.SqlDataReader> 实例选择两行，每行包含一个 `xml` 列   。 对于每一行，`xml` 列的值是使用 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 方法进行读取。 此值存储在 <xref:System.Xml.XmlReader> 中。 请注意，若要将内容设置为 <xref:System.Data.SqlTypes.SqlXml> 变量，必须使用 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlXml%2A>，而不是 <xref:System.Data.IDataRecord.GetValue%2A> 方法；<xref:System.Data.IDataRecord.GetValue%2A> 以字符串形式返回 `xml` 列的值。  
  
> [!NOTE]
>  默认情况下，在安装 SQL Server 时不安装 AdventureWorks 示例数据库  。 可以通过运行 SQL Server 安装程序来安装它。  
  
[!code-csharp [SqlDataReader_GetSqlXml#1](~/../sqlclient/doc/samples/SqlDataReader_GetSqlXml.cs#1)]
  
## <a name="next-steps"></a>后续步骤
- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server 中的 XML 数据](xml-data-sql-server.md)
