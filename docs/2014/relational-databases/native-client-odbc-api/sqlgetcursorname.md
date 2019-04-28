---
title: SQLGetCursorName | Microsoft Docs
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
ms.openlocfilehash: 603a2b5be4ca75495f094aa838d0373a9689a523
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657772"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  如果应用程序未指定游标名称， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将生成一个游标时的应用程序。 应用程序可以使用**SQLGetCursorName**要检索的驱动程序定义的游标名称定位的 UPDATE 和 DELETE 语句。 应用程序不需要调用**SQLSetCursorName**以利用定位数据操作语句。  
  
## <a name="see-also"></a>请参阅  
 [SQLGetCursorName 函数](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
