---
title: SQLNumResultCols |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: rothja
ms.author: jroth
ms.openlocfilehash: 45e72165eef621dc377b02ed3d2e7e1e3cf7ab8e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021866"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  对于执行的语句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序不会访问服务器来报告结果集中的列数。 在这种情况下，不 `SQLNumResultCols` 会导致服务器往返。 与[SQLDescribeCol](sqldescribecol.md)和[SQLColAttribute](sqlcolattribute.md)相似， `SQLNumResultCols` 对已准备但未执行的语句调用会生成服务器往返。  
  
 当某个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句批处理返回多个结果行集时，结果集列的个数可能在各个集之间有所变化。 `SQLNumResultCols`应为每个集调用。 如果列数有变化，应用程序应该在提取行结果之前重新绑定数据值。 有关处理多个结果集返回的详细信息，请参阅[SQLMoreResults](sqlmoreresults.md)。  
  
 从 "允许 SQLNumResultCols" 开始，数据库引擎中的改进 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可获取预期结果的更准确说明。 更准确的结果可能与早期版本的 SQLNumResultCols 返回的值不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLNumResultCols 函数](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
