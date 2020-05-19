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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7e9161170665d421b235a3a121ab8bb761e32daf
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706068"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  如果应用程序未指定游标名称，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序会在游标生成时为应用程序生成一个游标名称。 应用程序可以使用**SQLGetCursorName**来检索用于定位的 UPDATE 和 DELETE 语句的驱动程序定义的游标名称。 应用程序无需调用**SQLSetCursorName**来利用定位的数据操作语句。  
  
## <a name="see-also"></a>另请参阅  
 [SQLGetCursorName 函数](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
