---
title: SQLGetCursorName |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fc982405e1e5244b6d151c7475024590682cbc6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48114580"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  如果应用程序未指定游标名称， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将生成一个游标时的应用程序。 应用程序可以使用**SQLGetCursorName**要检索的驱动程序定义的游标名称定位的 UPDATE 和 DELETE 语句。 应用程序不需要调用**SQLSetCursorName**以利用定位数据操作语句。  
  
## <a name="see-also"></a>请参阅  
 [SQLGetCursorName 函数](http://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
