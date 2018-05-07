---
title: 使用 IOpenRowset 创建行集 |Microsoft 文档
description: 使用的 OLE DB 驱动程序的 IOpenRowset 接口 for SQL Server 创建一个行集合
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d518a5e7f2b4f5823317f20bd1669d8bd3adeeb7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="creating-a-rowset-with-iopenrowset"></a>使用 IOpenRowset 创建行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序支持**IOpenRowset::OpenRowset**方法有以下限制：  
  
-   基表或视图必须指定数据库中 ID (DBID) 结构的*pTableID*参数指向。  
  
-   DBID *eKind*成员必须指示 DBKIND_NAME。  
  
-   DBID *uName*成员必须为 Unicode 字符字符串中指定现有的基础表或视图的名称。  
  
-   *PIndexID*参数**OpenRowset**必须为 NULL。  
  
 结果集的**IOpenRowset::OpenRowset**包含单个行集。 可以通过支持包含单个行集的结果集[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]游标。 游标支持允许开发人员使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 并发控制机制。  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
