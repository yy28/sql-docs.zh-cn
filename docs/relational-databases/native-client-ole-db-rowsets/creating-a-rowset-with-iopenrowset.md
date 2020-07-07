---
title: 使用 IOpenRowset 创建行集 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5183d413e05fae6963ad0d314ba025a74edad3a9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005240"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>使用 IOpenRowset 创建行集
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序支持**IOpenRowset：： OpenRowset**方法，但有以下限制：  
  
-   必须在 pTableID 参数指向的数据库 ID (DBID) 结构中指定基表或视图**。  
  
-   DBID eKind 成员必须指示 DBKIND_NAME**。  
  
-   DBID uName 成员必须将现有基表或视图的名称指定为 Unicode 字符串**。  
  
-   OpenRowset 的 pIndexID 参数必须为 NULL******。  
  
 IOpenRowset::OpenRowset 的结果集包含单个行集****。 游标可以支持包含单个行集的结果集 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 游标支持允许开发人员使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并发控制机制。  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
