---
title: 使用服务器游标 |Microsoft 文档
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
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 689df4a5d8201fa6f7f59ead9ce87de01e0cd705
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126295"
---
# <a name="using-server-cursors"></a>使用服务器游标
  如果 ODBC 应用程序将任何 ODBC 游标特性设置为默认值，以外的任何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序会请求服务器以实现同一类型的 API 服务器游标。 如果使用 API 服务器游标，将在客户端上释放内存，并且可以大幅减少客户端与服务器之间的网络通信量。  
  
 API 服务器游标的潜在缺点是它们当前不支持所有 SQL 语句。 API 服务器游标无法用于执行：  
  
-   返回多个结果集的批处理或存储过程。  
  
-   包含 COMPUTE、COMPUTE BY、FOR BROWSE 或 INTO 子句的 SELECT 语句。  
  
-   引用远程存储过程的 EXECUTE 语句。  
  
 连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例时，如果使用服务器游标执行具有这些特征的语句，将导致游标转换到默认结果集。 连接到较早版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时，它将导致错误。  
  
## <a name="see-also"></a>请参阅  
 [如何实现游标](how-cursors-are-implemented.md)  
  
  