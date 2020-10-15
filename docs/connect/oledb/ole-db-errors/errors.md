---
title: OLE DB Errors
description: 了解 OLE DB Driver for SQL Server 中如何返回错误，以及你如何获取错误相关信息。
ms.custom: ''
ms.date: 05/06/2020
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f806ff605b8f35f112de4c16216e0da24d2df31c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081996"
---
# <a name="errors"></a>错误
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE/COM 对象通过对象成员函数的 HRESULT 返回代码报告错误。 OLE/COM HRESULT 是一种位压缩结构。 OLE 提供取消对结构成员的引用的宏。  
  
 OLE/COM 指定 IErrorInfo 接口  。 该接口公开 GetDescription 之类的方法  。 这允许客户端从 OLE/COM 服务器提取错误详细信息。 OLE DB 扩展 IErrorInfo 以支持返回针对单成员函数执行的多个错误信息包  。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以返回多个错误。 通过调用 [IMultipleResults::GetResult](/previous-versions/windows/desktop/ms721289(v=vs.85)) 并结合 ISQLErrorInfo 和 IErrorRecords，应用程序可以一次检索一个服务器错误。  
  
 适用于 SQL Server 的 OLE DB 驱动程序公开 OLE DB 记录增强型 IErrorInfo、自定义 ISQLErrorInfo 和特定于访问接口的 [ISQLServerErrorInfo](../ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md) 错误对象接口   。  
  
 有关跟踪错误的详细信息，请参阅[数据访问跟踪](/previous-versions/sql/sql-server-2008/cc765421(v=sql.100))。 有关 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中添加的错误跟踪的增强功能的信息，请参阅[访问扩展事件日志中的诊断信息](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [返回代码](../../oledb/ole-db-errors/return-codes.md)  
  
-   [错误接口中的信息](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 错误详细信息](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [检索错误信息](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 消息结果](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
