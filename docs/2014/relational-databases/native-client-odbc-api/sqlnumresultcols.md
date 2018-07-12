---
title: SQLNumResultCols |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c1a4825dc8d73f815f6b399c6e3a51c064d3b9b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424316"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  对于执行的语句， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序并不访问服务器以报告结果集中的列数。 在这种情况下，`SQLNumResultCols`不会导致服务器往返。 像[SQLDescribeCol](sqldescribecol.md)并[SQLColAttribute](sqlcolattribute.md)，则调用`SQLNumResultCols`对准备但不是执行的语句产生服务器往返。  
  
 当某个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句批处理返回多个结果行集时，结果集列的个数可能在各个集之间有所变化。 `SQLNumResultCols` 应该为每个集都调用。 如果列数有变化，应用程序应该在提取行结果之前重新绑定数据值。 有关详细信息，了解如何处理多个结果集返回，请参阅[SQLMoreResults](sqlmoreresults.md)。  
  
 从数据库引擎中的改进[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]允许 SQLNumResultCols 若要获取的预期的结果更准确描述。 这些更准确的结果可能不同于 SQLNumResultCols 的早期版本中返回的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[元数据发现](../native-client/features/metadata-discovery.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLNumResultCols 函数](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
