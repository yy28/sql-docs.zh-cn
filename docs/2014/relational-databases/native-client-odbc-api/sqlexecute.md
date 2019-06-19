---
title: SQLExecute | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ad659cfb929ac5a489b069db0b6a5f2b8abdae7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067493"
---
# <a name="sqlexecute"></a>SQLExecute
  如果语句属性 SQL_SOPT_SS_PARAM_FOCUS 未设置为 0，SQLExecute 将返回 SQL_ERROR 并生成的诊断记录具有 SQLSTATE = HY024 和消息"属性值无效，SQL_SOPT_SS_PARAM_FOCUS （必须在执行时为零）"。 有关 SQL_SOPT_SS_PARAM_FOCUS 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
## <a name="remarks"></a>备注  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=80708)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
