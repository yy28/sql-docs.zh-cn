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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33c33cf56490784e7cdfab3c37122f6317273e69
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003510"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  在手动提交模式中，对具有打开的事务的语句句柄调用**SQLFreeHandle**会导致对数据库的挂起的更改回滚。 对语句句柄调用**SQLFreeHandle**将始终关闭任何打开的游标，并放弃挂起的结果，释放与该语句句柄关联的所有资源。  
  
## <a name="see-also"></a>另请参阅  
 [SQLFreeHandle 函数](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
