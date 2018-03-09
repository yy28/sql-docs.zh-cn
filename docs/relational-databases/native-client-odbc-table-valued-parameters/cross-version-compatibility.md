---
title: "跨版本兼容性 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3fd2c2240e014fa4b7ff9d51ce94419b6cde839a
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="cross-version-compatibility"></a>跨版本兼容性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  如果期望让早于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 客户端或服务器实例处理表值参数，则会发生跨版本冲突。  
  
 通常，表值参数功能仅对连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）服务器的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 客户端（使用 SQL Server Native Client 10.0）或更高版本可用。 目录函数结果集中的新列将只能连接到时存在[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本） 服务器。  
  
 如果用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的更早版本编译的客户端应用程序执行了期望表值参数的语句，则服务器将通过数据转换错误检测到此情况，并且 ODBC 将以 SQLSTATE 07006 和消息“受限制的数据类型属性冲突”返回该错误。  
  
 如果客户端应用程序用编译[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 10.0 或更高版本尝试使用表值参数时连接到服务器实例早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端将检测到这，和 SQLBindCol，SQLBindParameter、 SQLSetDescFields 和 SQLSetDescRec 调用将失败，SQLSTATE 07006 和消息"限制 （此连接的 SQL Server 的版本不支持表值参数） 的数据类型属性冲突"。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
