---
title: 跨版本兼容性 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7990072ac539addf733720fd8c1eaba0652f5d70
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304498"
---
# <a name="cross-version-compatibility"></a>跨版本兼容性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  如果期望让早于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 客户端或服务器实例处理表值参数，则会发生跨版本冲突。  
  
 通常，表值参数功能仅对连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）服务器的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 客户端（使用 SQL Server Native Client 10.0）或更高版本可用。 仅当连接到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] （或更高版本）服务器时，才会显示目录函数结果集中的新列。  
  
 如果用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的更早版本编译的客户端应用程序执行了期望表值参数的语句，则服务器将通过数据转换错误检测到此情况，并且 ODBC 将以 SQLSTATE 07006 和消息“受限制的数据类型属性冲突”返回该错误。  
  
 如果使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client 10.0 或更高版本编译的客户端应用程序在连接到早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的服务器实例时尝试使用表值参数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则 Native client 将检测到此情况，而 SQLBindCol、SQLBindParameter、SQLSetDescFields 和 SQLSetDescRec 调用将失败，并出现 SQLSTATE 07006 和消息 "受限制的数据类型属性（此连接的 SQL Server 版本不支持表值参数）"。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;&#40;表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
