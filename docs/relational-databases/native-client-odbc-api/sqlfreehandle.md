---
title: SQLFreeHandle |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74f537c6017a2d8d247200ceccbd0faacb125cac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47595925"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在手动提交模式下，调用**SQLFreeHandle**语句上使用打开的事务句柄会导致挂起的更改回滚到数据库。 调用**SQLFreeHandle**语句句柄始终关闭任何打开的游标并放弃挂起的结果，释放语句句柄关联的所有资源。  
  
## <a name="see-also"></a>请参阅  
 [SQLFreeHandle 函数](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
