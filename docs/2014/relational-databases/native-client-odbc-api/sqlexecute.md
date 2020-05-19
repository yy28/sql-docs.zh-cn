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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ac50a5abd1f7e87017c6f0c559887b1796032328
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706127"
---
# <a name="sqlexecute"></a>SQLExecute
  如果语句属性 SQL_SOPT_SS_PARAM_FOCUS 未设置为0，则 SQLExecute 将返回 SQL_ERROR 并生成包含 SQLSTATE = HY024 的诊断记录和消息 "属性值无效，SQL_SOPT_SS_PARAM_FOCUS （在执行时必须为零）"。 有关 SQL_SOPT_SS_PARAM_FOCUS 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
## <a name="remarks"></a>备注  
 有关表值参数的详细信息，请参阅[ODBC&#41;&#40;表值参数](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=80708)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
