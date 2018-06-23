---
title: SQLExecute |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c422b06c23e2d8f42c48b3b7e03525e285db2769
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017090"
---
# <a name="sqlexecute"></a>SQLExecute
  如果： SQL_SOPT_SS_PARAM_FOCUS 没有设置为 0，SQLExecute 语句属性将返回 SQL_ERROR 和生成的诊断记录 SQLSTATE = HY024 和消息"无效的属性值： SQL_SOPT_SS_PARAM_FOCUS （必须在执行时的零）"。 : SQL_SOPT_SS_PARAM_FOCUS 有关的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
## <a name="remarks"></a>Remarks  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=80708)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  