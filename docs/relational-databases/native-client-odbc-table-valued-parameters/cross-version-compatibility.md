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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d1979d090ea01648f36ee0ee20b6aa7aa2138cbc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617795"
---
# <a name="cross-version-compatibility"></a>跨版本兼容性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  如果期望让早于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 客户端或服务器实例处理表值参数，则会发生跨版本冲突。  
  
 通常，表值参数功能仅对连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本）服务器的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 客户端（使用 SQL Server Native Client 10.0）或更高版本可用。 目录函数结果集中的新列才会显示在连接到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更高版本） 服务器。  
  
 如果用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的更早版本编译的客户端应用程序执行了期望表值参数的语句，则服务器将通过数据转换错误检测到此情况，并且 ODBC 将以 SQLSTATE 07006 和消息“受限制的数据类型属性冲突”返回该错误。  
  
 如果使用已编译的客户端应用程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 10.0 或更高版本尝试使用表值参数时连接到服务器实例早于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端将检测到这，和 SQLBindCol，SQLBindParameter、 SQLSetDescFields 和 SQLSetDescRec 调用将失败，SQLSTATE 07006 和消息"受限制的数据类型属性冲突 （为此连接的 SQL Server 的版本不支持表值参数）"。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
