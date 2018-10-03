---
title: 错误 |Microsoft Docs
description: 错误
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: cbc69702105ece1e2406ebda9be4f906cc27585a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643085"
---
# <a name="errors"></a>错误
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE/COM 对象通过对象成员函数的 HRESULT 返回代码报告错误。 OLE/COM HRESULT 是一种位压缩结构。 OLE 提供取消对结构成员的引用的宏。  
  
 OLE/COM 指定 IErrorInfo 接口。 该接口公开 GetDescription 之类的方法。 这允许客户端从 OLE/COM 服务器提取错误详细信息。 OLE DB 扩展 IErrorInfo 以支持返回针对单成员函数执行的多个错误信息包。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以返回多个错误。 通过调用 [IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630) 并结合 ISQLErrorInfo 和 IErrorRecords，应用程序可以一次检索一个服务器错误。  
  
 适用于 SQL Server 的 OLE DB 驱动程序公开 OLE DB 记录增强型 IErrorInfo、自定义 ISQLErrorInfo 和特定于访问接口的 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 错误对象接口。  
  
 有关跟踪错误的详细信息，请参阅[数据访问跟踪](http://go.microsoft.com/fwlink/?LinkId=125805)。 有关添加中的错误跟踪的增强功能的信息[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，请参阅[访问扩展事件日志中的诊断信息](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [返回代码](../../oledb/ole-db-errors/return-codes.md)  
  
-   [错误接口中的信息](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 错误详细信息](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [检索错误信息](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 消息结果](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
