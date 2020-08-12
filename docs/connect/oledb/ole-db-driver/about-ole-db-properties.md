---
title: 关于 OLE DB 连接属性 | Microsoft Docs
description: 关于 OLE DB 属性
ms.custom: ''
ms.date: 05/20/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, properties
- OLE DB Driver for SQL Server, properties
- properties [OLE DB]
- property values [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: fa2fbb56d9d8926c45970ecddfabd226c87d26e2
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004458"
---
# <a name="about-ole-db-properties"></a>关于 OLE DB 属性
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

<!--
NOTE , GeneMi , 2020/May/20:
    This SQL 2016+ article is a nearly exact duplicate of another SQL 2016+ article.
    This article resides under docs/connect/oledb/ole-db-driver/.

    The other article resides under docs/relational-databases/native-client-ole-db-provider/.
    And, the other article has a SQL 2014 counterpart having its same GitHub directory path and filename, to support SQL 2014 OPS Versioning with SQL 2016+.

    This path-file name is:
'\sql-docs-pr\docs\connect\oledb\ole-db-driver\about-ole-db-properties.md'.

    The other path-file is named:
'\sql-docs-pr\docs\relational-databases\native-client-ole-db-provider\about-ole-db-properties.md'.

    Therefore, maybe this docs/connect/oledb/... file should be deleted?

1611957:  This NOTE relates to SEO content bug 1611957 about metadata 'title:' value duplication:
    https://mseng.visualstudio.com/TechnicalContent/_workitems/edit/1611957

PR 15068:  This HTML comment is being added by PR...
    https://github.com/MicrosoftDocs/sql-docs-pr/pull/15068
-->

  使用者设置属性值以请求特定的对象行为。 例如，使用者使用属性以指定要由行集公开的接口。 使用者获得属性值，以确定对象（比如行集、会话或数据源对象）的功能。  
  
 每个属性都有值、类型、说明和读/写属性，对于行集属性，还有一个用于指示是否可以逐列应用它的指示器。  
  
 属性由一个 GUID 和一个表示属性 ID 的整数进行标识。 属性集是所有具有相同 GUID 的一组属性。 除了预定义的 OLE DB 属性集以外，适用于 SQL Server 的 OLE DB 驱动程序还实现了特定于访问接口的属性集和属性集中的属性。 每个属性属于一个或多个属性组。 属性组是应用于特定对象的所有属性所形成的组。 属性组包括初始化属性组、数据源属性组、会话属性组、行集属性组、表属性组和列属性组等等。 在每个这样的属性组中都有属性。  
  
 设置属性值涉及：  
  
1.  确定要设置值的属性。  
  
2.  确定包含所标识属性的属性集。  
  
3.  分配 DBPROPSET 结构数组，每个标识的属性集一个。  
  
4.  为每个属性集分配 DBPROP 结构数组。 每个数组中的元素个数是属于该属性集的属性（在步骤 1 中标识）的个数。  
  
5.  填充每个属性的 DBPROP 结构。  
  
6.  在每个属性集的 DBPROPSET 结构中，填充信息（属性集 GUID、元素的计数以及对应的 DBPROP 数组的指针）。  
  
7.  调用方法以设置属性，并传递 DBPROPSET 结构的计数和数组。  
  
## <a name="see-also"></a>另请参阅  
 [创建适用于 SQL Server 的 OLE DB 驱动程序应用程序](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [属性 (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=112207)  
  
  
