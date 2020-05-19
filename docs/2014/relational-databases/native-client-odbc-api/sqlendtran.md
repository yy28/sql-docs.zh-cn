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
manager: craigg
ms.openlocfilehash: ec3c40d7821c86f3f5c5a7eb0d63ab48904513e2
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706264"
---
# <a name="sqlendtran"></a>SQLEndTran
  默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在**SQLEndTran**提交或回滚操作时，Native Client ODBC 驱动程序会关闭语句的关联游标。 服务器游标将关闭，除非它们是静态的。 当**SQLEndTran**提交或回滚操作时，语句的关联游标的行为取决于驱动程序特定的 ODBC 连接属性的值，SQL_COPT_SS_PRESERVE_CURSORS，由[SQLSetConnectAttr](sqlsetconnectattr.md)设置。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 实现细节](odbc-api-implementation-details.md)   
 [SQLEndTran 函数](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
