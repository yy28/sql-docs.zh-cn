---
title: 大型 CLR 用户定义类型 |Microsoft 文档
description: 大型 CLR 用户定义类型 OLE DB 驱动程序中的 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 98efe44495c73aef6baf030eb2ea4b4b11ab4e7c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="large-clr-user-defined-types"></a>大型 CLR 用户定义类型
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在 SQL Server 2005 中，公共语言运行时 (CLR) 中的用户定义类型 (UDT) 已限制为最大 8,000 字节。 这一限制在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 和更高版本中已取消。 CLR UDT 现在以针对大型对象 (LOB) 类型的类似方式处置。 也就是说，小于或等于 8,000 字节的 UDT 在行为上与 SQL Server 2005 中相同，但支持更大的 UDT 并且将其大小报告为“无限制”。  
  
 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;OLE DB&#41;](../../oledb/ole-db/large-clr-user-defined-types-ole-db.md)。  
  
## <a name="use-cases"></a>用例   
  
 有关 OLE DB，支持大型 Udt 的使用 ISequentialStream 绑定包括为流 UDT 值与服务器的功能。  
  
 小于或等于 8,000 字节的 UDT 在行为上与 SQL Server 2005 中相同。 用于 OLE DB，你仍可以通过使用 ISequentialStream 绑定流小 Udt。  
  
 有时候，本机代码将必须理解 CLR UDT 的内容，但将不必实例化托管对象。 在此情况下，您可以使用自定义序列化将服务器上的 UDT 值转换为客户端的已知格式。  
  
 对于具有现有数据访问代码的应用程序，您可以通过在本机 API 中检索 UDT 并通过在混合模式应用程序中使用 C++ CLI interop 实例化它们，在客户端上利用 CLR UDT 行为。  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../../oledb/features/oledb-driver-for-sql-server-features.md)    
  
  
