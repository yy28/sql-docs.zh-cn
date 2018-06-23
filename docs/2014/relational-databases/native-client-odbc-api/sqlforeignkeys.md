---
title: SQLForeignKeys |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
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
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 20b48d67072919fe42661343ff133cd3ea1a8773
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128754"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过外键约束机制支持级联更新和删除操作。 如果在 FOREIGN KEY 约束的 ON UPDATE 和/或 ON DELETE 子句中指定 CASCADE 选项，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将为 UPDATE_RULE 和/或 DELETE_RULE 列返回 SQL_CASCADE。 如果未在 FOREIGN KEY 约束的 ON UPDATE 和/或 ON DELETE 子句中指定 NO ACTION 选项，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 则为 UPDATE_RULE 和/或 DELETE_RULE 列返回 SQL_NO_ACTION。  
  
 在任何中存在无效的值时**SQLForeignKeys**参数， **SQLForeignKeys**返回 SQL_SUCCESS 上执行。 **SQLFetch**返回 SQL_NO_DATA，在这些参数中使用了无效值。  
  
 **SQLForeignKeys**可以执行对静态服务器游标。 尝试执行**SQLForeignKeys**返回的可更新的 （动态或键集） 游标中的 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持为链接服务器上的表报表信息由接受的两部分名称*FKCatalogName*和*PKCatalogName*参数： *Linked_Server_Name.Catalog_Name*。  
  
## <a name="see-also"></a>请参阅  
 [SQLForeignKeys 函数](http://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  