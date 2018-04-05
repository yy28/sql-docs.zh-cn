---
title: SQLRateConnection 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 22f7e5c4181a0b36a862ab0e0b819891a3dee9fe
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 函数
**一致性**  
 版本引入了： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLRateConnection**确定驱动程序是否可以重用连接池中现有的连接。  
  
## <a name="syntax"></a>语法  
  
```  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>参数  
 *hRequest*  
 [输入]一个表示新的应用程序连接请求令牌的句柄。  
  
 *hCandidateConnection*  
 [输入]中的连接池的现有连接。 连接必须处于打开状态。  
  
 *fRequiredTransactionEnlistment*  
 [输入]如果为 TRUE，则重用现有连接的*hCandidateConnection*用于新连接请求 (*hRequest*) 需要的其他登记。  
  
 *transId*  
 [输入]如果*fRequiredTransactionEnlistment*为 TRUE， *transId*表示请求会登记的 DTC 事务。 如果*fRequiredTransactionEnlistment*为 FALSE 时， *transId*将被忽略。  
  
 *pRating*  
 [输出]*hCandidateConnection*的重用评级对*hRequest*。 此级别将 0 和 100 （含） 之间。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 驱动程序管理器将不处理此函数返回的诊断信息。  
  
## <a name="remarks"></a>Remarks  
 **SQLRateConnection**生成介于 0 和 100 （含），该值指示一个现有的连接与请求匹配的程度之间的分数。  
  
|分数|含义 （如果返回 SQL_SUCCESS）|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection*不能将重复使用的*hRequest*。|  
|介于 1 和 98 （含） 之间的任何值|分数越高，越接近， *hCandidateConnection*与匹配*hRequest*。|  
|99|无意义的属性中有仅不匹配。  驱动程序管理器应停止分级循环。|  
|100|完全匹配。  驱动程序管理器应停止分级循环。|  
|大于 100 的任何其他值|*hCandidateConnection*标记为死和它将不能重复使用即使在将来连接请求。|  
  
 如果返回的代码是 SQL_SUCCESS （包括 SQL_SUCCESS_WITH_INFO） 之外的任何或分级大于 100，驱动程序管理器会将标记为失效的连接。 该死连接将不重用 （即使在将来连接请求），并且最终将在之后将传递 CPTimeout 已超时。 驱动程序管理器将继续查找从池到速率的另一个连接。  
  
 如果驱动程序管理器重复使用其评分是严格小于 100 （包括 99） 的连接，驱动程序管理器将调用 SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) 以重置该连接返回到该应用程序请求的状态。 驱动程序不应重置此函数调用中的连接。  
  
 如果*fRequiredTransactionEnlistment*为 TRUE，那么重复使用*hCandidateConnection*需要的额外登记 (*transId* ！ = NULL) 或征用 (*transId* = = NULL)。 这指示重用连接和是否驱动程序应登记 / 取消登记连接，如果它要重复使用连接的成本。 如果*fRequireTransactionEnlistment*为 FALSE 时，驱动程序应忽略的值*transId*。  
  
 驱动程序管理器可保证 HENV 处理的父*hRequest*和*hCandidateConnection*相同。 驱动程序管理器可保证与关联的池 ID *hRequest*和*hCandidateConnection*相同。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h ODBC 驱动程序的开发。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
