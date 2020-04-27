---
title: SQLFreeHandle |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 197d3e1d36f8513821cec9630cade8f52681a43d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63154660"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  在手动提交模式中，对具有打开的事务的语句句柄调用**SQLFreeHandle**会导致对数据库的挂起的更改回滚。 对语句句柄调用**SQLFreeHandle**将始终关闭任何打开的游标，并放弃挂起的结果，释放与该语句句柄关联的所有资源。  
  
## <a name="see-also"></a>另请参阅  
 [SQLFreeHandle 函数](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
