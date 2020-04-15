---
title: SQLRate连接功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d29033460a7f89fc4a8b1c371a4d32bdf94a2a05
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288877"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 函数
**一致性**  
 版本介绍： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLRateConnection**确定驱动程序是否可以重用连接池中的现有连接。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>参数  
 *h请求*  
 [输入]表示新应用程序连接请求的令牌句柄。  
  
 *h候选人连接*  
 [输入]连接池中的现有连接。 连接必须处于打开状态。  
  
 *f 必需交易登记*  
 [输入]如果为 TRUE，则重新使用现有连接的*h候选连接*以执行新的连接请求 *（hRequest*） 需要额外的登记。  
  
 *转体*  
 [输入]如果*f需要交易登记*为 TRUE，transId 表示请求将登记的 DTC 事务。 *transId* 如果*f"需要交易登记"* 为 FALSE，则将忽略*transId。*  
  
 *放大缩小字体功能 放大缩小字体功能*  
 [输出]*h候选连接*的重新使用等级为*hRequest*。 此评级将在 0 和 100 之间（含）。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 驱动程序管理器不会处理从此功能返回的诊断信息。  
  
## <a name="remarks"></a>备注  
 **SQLRateConnection**生成介于 0 和 100（含）之间的分数，指示现有连接与请求匹配程度。  
  
|Score|含义（返回SQL_SUCCESS时）|  
|-----------|-----------------------------------------------|  
|0|*h候选连接*不得为*hRequest*重复使用。|  
|介于 1 和 98 之间的任何值（含）|分数越高 *，h候选连接*与*hRequest*匹配越近。|  
|99|在微不足道的属性中，只有不匹配。  驱动程序管理器应停止评级循环。|  
|100|完美匹配。  驱动程序管理器应停止评级循环。|  
|任何其他大于 100 的值|*h候选连接*标记为已死，即使在将来的连接请求中也不会重复使用。|  
  
 如果返回代码不是SQL_SUCCESS（包括SQL_SUCCESS_WITH_INFO）或额定值大于 100，则驱动程序管理器将连接标记为已死。 连接不会重复使用（即使在将来的连接请求中），并且最终将在 CPTimeout 通过后超时。 驱动程序管理器将继续从池中查找另一个连接以进行速率。  
  
 如果驱动程序管理器重用分数严格小于 100（包括 99）的连接，驱动程序管理器将调用 SQLSetConnectAttr（SQL_ATTR_DBC_INFO_TOKEN）将连接重新重置为应用程序请求的状态。 驱动程序不应在此函数调用中重置连接。  
  
 如果*f"必需交易登记"* 为 TRUE，则重用*h候选连接*需要额外的登记（*转接*！= NULL）或取消登记（*转 Id* = NULL）。 这表示重用连接的成本，以及驱动程序是否应登记/取消登记连接（如果该连接要重用连接）。 如果*f要求事务登记*为 FALSE，驱动程序应忽略*transId*的值。  
  
 驱动程序管理器保证*hRequest*和*h候选连接*的父 HENV 句柄相同。 驱动程序管理器保证与*hRequest*和*h候选连接*关联的池 ID 相同。  
  
 应用程序不应直接调用此功能。 支持驱动程序感知连接池的 ODBC 驱动程序必须实现此功能。  
  
 包括用于 ODBC 驱动程序开发的 sqlspi.h。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
