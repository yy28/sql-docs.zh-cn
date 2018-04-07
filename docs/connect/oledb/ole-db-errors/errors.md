---
title: 错误 |Microsoft 文档
description: 错误
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b2ce3a7470391bc35acd3004f08db8f04a5eae2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="errors"></a>错误
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE/COM 对象通过对象成员函数的 HRESULT 返回代码报告错误。 OLE/COM HRESULT 是一种位压缩结构。 OLE 提供取消对结构成员的引用的宏。  
  
 OLE/COM 指定**IErrorInfo**接口。 该接口公开方法，如**GetDescription**。 这允许客户端从 OLE/COM 服务器提取错误详细信息。 OLE DB 扩展**IErrorInfo**以支持单成员函数执行返回的多个错误信息数据包。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以返回多个错误。 应用程序可以检索服务器错误一次通过调用[IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630)与 ISQLErrorInfo 和 IErrorRecords 的组合。  
  
 SQL Server 的 OLE DB 驱动程序公开 OLE DB 记录增强**IErrorInfo**，自定义**ISQLErrorInfo**，和特定于提供程序的[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)错误对象接口。  
  
 有关跟踪错误的信息，请参阅[数据访问跟踪](http://go.microsoft.com/fwlink/?LinkId=125805)。 有关在中添加的错误跟踪的增强功能[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，请参阅[访问扩展事件日志中的诊断信息](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [返回代码](../../oledb/ole-db-errors/return-codes.md)  
  
-   [错误接口中的信息](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 错误详细信息](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [检索错误信息的信息](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 消息结果](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 的 OLE DB 驱动程序&#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
