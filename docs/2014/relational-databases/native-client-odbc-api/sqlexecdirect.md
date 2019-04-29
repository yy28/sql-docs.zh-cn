---
title: SQLExecDirect | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecDirect function
ms.assetid: e7c2a5b5-83f4-4c72-9aca-7b9fb4748b11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f9e4790cfae631a9a977431f25282aae766f3e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63067504"
---
# <a name="sqlexecdirect"></a>SQLExecDirect
  如果语句属性 SQL_SOPT_SS_PARAM_FOCUS 不为 0，SQLExecDirect 将返回 SQL_ERROR 并生成的诊断记录具有 SQLSTATE = HY024 和消息"属性值无效，SQL_SOPT_SS_PARAM_FOCUS （必须在执行时为零）"。 有关 SQL_SOPT_SS_PARAM_FOCUS 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=80709)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
