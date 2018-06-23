---
title: SQLFreeHandle |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8ba108cf9efcd6e7e8fd91ccc026fe616c113d1d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125093"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  在手动提交模式下，调用**SQLFreeHandle**在语句句柄与打开的事务会导致挂起的更改到数据库的回滚。 调用**SQLFreeHandle**基于语句句柄始终关闭所有打开的游标并放弃挂起的结果，释放与该语句句柄关联的所有资源。  
  
## <a name="see-also"></a>请参阅  
 [SQLFreeHandle 函数](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  