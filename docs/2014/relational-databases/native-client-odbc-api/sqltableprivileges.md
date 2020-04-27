---
title: SQLTablePrivileges |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51492e55fd3c34c099a5f53187d1b2a9875ce7e3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63188638"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
  可以对静态游标执行**SQLTablePrivileges** 。 尝试对可更新的（键集驱动或动态）执行**SQLTablePrivileges**将返回 SQL_SUCCESS_WITH_INFO 指示游标类型已更改。  
  
 Native Client ODBC 驱动程序通过接受由两部分组成的*CatalogName*参数的名称来支持链接服务器上表的报告信息： *Linked_Server_Name。 Catalog_Name。* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [SQLTablePrivileges 函数](https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
