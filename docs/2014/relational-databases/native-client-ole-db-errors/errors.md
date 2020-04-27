---
title: 错误 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 434b4251c51809c97744e7aaf954ac1f11c06cfa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63050668"
---
# <a name="errors"></a>错误
  OLE/COM 对象通过对象成员函数的 HRESULT 返回代码报告错误。 OLE/COM HRESULT 是一种位压缩结构。 OLE 提供取消对结构成员的引用的宏。  
  
 OLE/COM 指定 IErrorInfo 接口****。 该接口公开 GetDescription 之类的方法****。 这允许客户端从 OLE/COM 服务器提取错误详细信息。 OLE DB 扩展 IErrorInfo 以支持返回针对单成员函数执行的多个错误信息包****。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以返回多个错误。 通过调用 [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) 并结合 ISQLErrorInfo 和 IErrorRecords，应用程序可以一次检索一个服务器错误。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开了 OLE DB 的增强型**IErrorInfo**、自定义`ISQLErrorInfo`和特定于提供程序的[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)错误对象接口。  
  
 有关跟踪错误的详细信息，请参阅[数据访问跟踪](https://go.microsoft.com/fwlink/?LinkId=125805)。 有关 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中添加的错误跟踪的增强功能的信息，请参阅[访问扩展事件日志中的诊断信息](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [返回代码](return-codes.md)  
  
-   [错误接口中的信息](information-in-error-interfaces.md)  
  
-   [SQL Server 错误详细信息](sql-server-error-detail.md)  
  
-   [检索错误信息](retrieving-error-information.md)  
  
-   [SQL Server 消息结果](sql-server-message-results.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
