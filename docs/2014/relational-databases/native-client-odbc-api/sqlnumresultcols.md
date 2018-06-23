---
title: SQLNumResultCols |Microsoft 文档
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
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 73ac3425eab1a4c19130352ef566153eb6c34e53
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016350"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  对于执行语句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不访问服务器报告的结果集中的列数。 在这种情况下，`SQLNumResultCols`不会导致服务器往返。 如[SQLDescribeCol](sqldescribecol.md)和[SQLColAttribute](sqlcolattribute.md)，则调用`SQLNumResultCols`在准备好但是未执行的语句会生成服务器往返。  
  
 当某个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句批处理返回多个结果行集时，结果集列的个数可能在各个集之间有所变化。 `SQLNumResultCols` 应为每个组调用。 如果列数有变化，应用程序应该在提取行结果之前重新绑定数据值。 有关处理多个结果集返回，请参阅[SQLMoreResults](sqlmoreresults.md)。  
  
 从数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 SQLNumResultCols 以获取更准确的预期结果的说明。 这些更准确的结果可能与在以前版本的 SQLNumResultCols 返回的值不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLNumResultCols 函数](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  