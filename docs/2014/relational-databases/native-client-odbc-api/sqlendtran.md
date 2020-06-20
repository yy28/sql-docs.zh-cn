---
title: SQLEndTran |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: rothja
ms.author: jroth
ms.openlocfilehash: e5d44756131b6133baec69e34da11055a965e2da
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022726"
---
# <a name="sqlendtran"></a>SQLEndTran
  默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在**SQLEndTran**提交或回滚操作时，Native Client ODBC 驱动程序会关闭语句的关联游标。 服务器游标将关闭，除非它们是静态的。 当**SQLEndTran**提交或回滚操作时，语句的关联游标的行为取决于驱动程序特定的 ODBC 连接属性的值，SQL_COPT_SS_PRESERVE_CURSORS，由[SQLSetConnectAttr](sqlsetconnectattr.md)设置。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 实现细节](odbc-api-implementation-details.md)   
 [SQLEndTran 函数](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
