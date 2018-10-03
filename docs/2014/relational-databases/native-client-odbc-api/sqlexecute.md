---
title: SQLExecute |Microsoft Docs
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
ms.openlocfilehash: fab0ac676e4d0fc1b9d74c4aa9d1e472b8316a7e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095288"
---
# <a name="sqlexecute"></a>SQLExecute
  如果语句属性 SQL_SOPT_SS_PARAM_FOCUS 未设置为 0，SQLExecute 将返回 SQL_ERROR 并生成的诊断记录具有 SQLSTATE = HY024 和消息"属性值无效，SQL_SOPT_SS_PARAM_FOCUS （必须在执行时为零）"。 有关 SQL_SOPT_SS_PARAM_FOCUS 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
## <a name="remarks"></a>备注  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=80708)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
