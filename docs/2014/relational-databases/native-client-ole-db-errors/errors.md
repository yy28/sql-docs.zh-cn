---
title: 错误 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac616813b3437c57a8e071ea876874880874f039
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424666"
---
# <a name="errors"></a>错误
  OLE/COM 对象通过对象成员函数的 HRESULT 返回代码报告错误。 OLE/COM HRESULT 是一种位压缩结构。 OLE 提供取消对结构成员的引用的宏。  
  
 OLE/COM 指定**IErrorInfo**接口。 该接口公开的方法，如**GetDescription**。 这允许客户端从 OLE/COM 服务器提取错误详细信息。 OLE DB 扩展**IErrorInfo**以支持单成员函数执行返回多个错误信息包。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以返回多个错误。 应用程序可以检索服务器错误一次通过调用[imultipleresults:: Getresult](http://go.microsoft.com/fwlink/?LinkId=129630)加上 ISQLErrorInfo 和 IErrorRecords。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开 OLE DB 记录增强型**IErrorInfo**，自定义`ISQLErrorInfo`，和特定于提供程序的[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)对象时出错接口。  
  
 有关跟踪错误的信息，请参阅[数据访问跟踪](http://go.microsoft.com/fwlink/?LinkId=125805)。 有关添加中的错误跟踪的增强功能的信息[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，请参阅[访问扩展事件日志中的诊断信息](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [返回代码](return-codes.md)  
  
-   [错误接口中的信息](information-in-error-interfaces.md)  
  
-   [SQL Server 错误详细信息](sql-server-error-detail.md)  
  
-   [检索错误信息](retrieving-error-information.md)  
  
-   [SQL Server 消息结果](sql-server-message-results.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (OLE DB)](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
