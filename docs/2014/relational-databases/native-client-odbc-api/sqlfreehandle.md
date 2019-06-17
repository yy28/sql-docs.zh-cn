---
title: SQLFreeHandle | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63154660"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  在手动提交模式下，调用**SQLFreeHandle**语句上使用打开的事务句柄会导致挂起的更改回滚到数据库。 调用**SQLFreeHandle**语句句柄始终关闭任何打开的游标并放弃挂起的结果，释放语句句柄关联的所有资源。  
  
## <a name="see-also"></a>请参阅  
 [SQLFreeHandle 函数](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
