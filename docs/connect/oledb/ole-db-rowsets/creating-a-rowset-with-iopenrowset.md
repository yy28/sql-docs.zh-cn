---
title: 使用 IOpenRowset (OLE DB driver) 创建行集 | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 如何支持 IOpenRowset::OpenRowset 方法以返回行集及对其使用的限制。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a39ff5a60f13a25c271be61d4db20a604364420
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862261"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>使用 IOpenRowset 创建行集
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 支持 IOpenRowset::OpenRowset  方法，但具有以下限制：  
  
-   必须在 pTableID 参数指向的数据库 ID (DBID) 结构中指定基表或视图  。  
  
-   DBID eKind 成员必须指示 DBKIND_NAME  。  
  
-   DBID uName 成员必须将现有基表或视图的名称指定为 Unicode 字符串  。  
  
-   OpenRowset 的 pIndexID 参数必须为 NULL   。  
  
 IOpenRowset::OpenRowset 的结果集包含单个行集  。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 游标可以支持包含单个行集的结果集。 游标支持允许开发人员使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 并发控制机制。  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
