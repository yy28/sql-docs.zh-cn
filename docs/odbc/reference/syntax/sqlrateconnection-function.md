---
title: SQLRateConnection 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d36224329fa29a54f7163cb4e1ce6228f460875
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262496"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 函数
**符合性**  
 版本引入了：ODBC 3.81 标准符合性：ODBC  
  
 **摘要**  
 **SQLRateConnection**确定驱动程序可以重用连接池中的现有连接。  
  
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
 [输入]中的连接池的现有连接。 该连接必须处于打开状态。  
  
 *fRequiredTransactionEnlistment*  
 [输入]如果为 TRUE，重复使用现有连接*hCandidateConnection*新的连接请求 (*hRequest*) 需要更多的登记。  
  
 *transId*  
 [输入]如果*fRequiredTransactionEnlistment*为 TRUE， *transId*表示该请求将登记 DTC 事务。 如果*fRequiredTransactionEnlistment*为 FALSE 时， *transId*将被忽略。  
  
 *pRating*  
 [输出]*hCandidateConnection*的重用级别对于*hRequest*。 此分级将是 0 到 100 之间 （含） 之间。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 驱动程序管理器不会处理从该函数返回的诊断信息。  
  
## <a name="remarks"></a>备注  
 **SQLRateConnection**生成介于 0 和 100 之间 （含），该值指示现有连接与请求的匹配程度之间的分数。  
  
|分数|含义 （时，将返回 SQL_SUCCESS）|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection*不能将重复使用的*hRequest*。|  
|介于 1 和 98 （含） 之间的任何值|分数越高，越接近， *hCandidateConnection*与匹配*hRequest*。|  
|99|无意义的属性中有仅不匹配。  驱动程序管理器应停止分级循环。|  
|100|完美匹配。  驱动程序管理器应停止分级循环。|  
|大于 100 的任何其他值|*hCandidateConnection*标记为停用以及它将不能重复使用甚至在将来连接请求。|  
  
 如果返回代码 （包括 SQL_SUCCESS_WITH_INFO） SQL_SUCCESS 以外的内容或分级大于 100，驱动程序管理器会将标记为不活动的连接。 死连接不会 （甚至在将来的连接请求） 重复使用，并最终将在之后 CPTimeout 传递已超时。 驱动程序管理器将继续查找从池到速率的另一个连接。  
  
 如果驱动程序管理器重复使用其分数是严格小于 100 （包括 99） 的连接，驱动程序管理器将调用 SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) 重置该连接返回到应用程序请求的状态。 该驱动程序不应重置此函数调用中的连接。  
  
 如果*fRequiredTransactionEnlistment*为 TRUE，那么重用*hCandidateConnection*需要的额外登记 (*transId* ！ = NULL) 或征用 (*transId* = = NULL)。 这表示的重复使用的连接和驱动程序是否应登记 / 取消登记连接，如果要重复使用连接的成本。 如果*fRequireTransactionEnlistment*为 FALSE 时，驱动程序应忽略的值*transId*。  
  
 驱动程序管理器可保证 HENV 处理的父*hRequest*并*hCandidateConnection*相同。 驱动程序管理器可保证与关联的池 ID *hRequest*并*hCandidateConnection*相同。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h 的 ODBC 驱动程序开发。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
