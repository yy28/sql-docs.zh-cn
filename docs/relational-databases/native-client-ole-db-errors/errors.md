---
description: SQL Server Native Client 错误
title: 错误 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8772533314f084e0ff9e6a8f3abaa860da772680
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448470"
---
# <a name="sql-server-native-client-errors"></a>SQL Server Native Client 错误
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  OLE/COM 对象通过对象成员函数的 HRESULT 返回代码报告错误。 OLE/COM HRESULT 是一种位压缩结构。 OLE 提供取消对结构成员的引用的宏。  
  
 OLE/COM 指定 IErrorInfo 接口  。 该接口公开 GetDescription 之类的方法  。 这允许客户端从 OLE/COM 服务器提取错误详细信息。 OLE DB 扩展 IErrorInfo 以支持返回针对单成员函数执行的多个错误信息包  。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以返回多个错误。 通过调用 [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) 并结合 ISQLErrorInfo 和 IErrorRecords，应用程序可以一次检索一个服务器错误。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序公开了 OLE DB 记录增强的**IErrorInfo**、自定义的**ISQLErrorInfo**，以及特定于提供程序的[ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15)错误对象接口。  
  
 有关跟踪错误的详细信息，请参阅[数据访问跟踪](https://go.microsoft.com/fwlink/?LinkId=125805)。 有关 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中添加的错误跟踪的增强功能的信息，请参阅[访问扩展事件日志中的诊断信息](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [返回代码](../../relational-databases/native-client-ole-db-errors/return-codes.md)  
  
-   [错误接口中的信息](../../relational-databases/native-client-ole-db-errors/information-in-error-interfaces.md)  
  
-   [SQL Server 错误详细信息](../../relational-databases/native-client-ole-db-errors/sql-server-error-detail.md)  
  
-   [检索错误信息](../../relational-databases/native-client-ole-db-errors/retrieving-error-information.md)  
  
-   [SQL Server 消息结果](../../relational-databases/native-client-ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
