---
title: SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed3bdb4cc5c2508435bff011545b5b9113d7aeac
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424386"
---
# <a name="sqlcancel"></a>SQLCancel
  [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)主题指出，在 ODBC 2.x 中，如果应用程序调用`SQLCancel`语句上不执行任何处理，是当`SQLCancel`具有相同的效果`SQLFreeStmt`与`SQL_CLOSE`选项; 这仅出于完整性的考虑定义行为和应用程序应调用`SQLFreeStmt`或`SQLCloseCursor`关闭游标。 但是，即使您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 应用程序将 ODBC API 版本设置为 3.5.x 或更高版本，`SQLCancel` 函数也将使用 ODBC 2.x 行为。  
  
## <a name="see-also"></a>请参阅  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
