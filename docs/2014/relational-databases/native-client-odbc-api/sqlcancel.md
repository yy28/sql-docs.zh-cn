---
title: SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bad2cc35a30f5c6f5855292ff73635cef6072b2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364259"
---
# <a name="sqlcancel"></a>SQLCancel
  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)主题指出，在 ODBC 2.x 中，如果应用程序调用`SQLCancel`语句上不执行任何处理，是当`SQLCancel`具有相同的效果`SQLFreeStmt`与`SQL_CLOSE`选项; 这仅出于完整性的考虑定义行为和应用程序应调用`SQLFreeStmt`或`SQLCloseCursor`关闭游标。 但是，即使您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 应用程序将 ODBC API 版本设置为 3.5.x 或更高版本，`SQLCancel` 函数也将使用 ODBC 2.x 行为。  
  
## <a name="see-also"></a>请参阅  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
