---
title: "连接选项 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bb45857d47ef145c5693f6718696cbf75ccd666
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connect-options"></a>连接选项
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 这些选项允许进行自定义应用程序中的数据库连接。  
  
|连接选项|说明|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|如果你选择 SQL_AUTOCOMMIT_OFF，你的应用程序必须显式提交或回滚的事务[SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)。|  
|SQL_ODBC_CURSORS|此连接属性实现驱动程序管理器中。|  
|SQL_OPT_TRACE|此连接属性实现驱动程序管理器中。|  
|SQL_OPT_TRACEFILE|此连接属性实现驱动程序管理器中。|  
|SQL_TRANSLATE_DLL|返回错误:"驱动程序不可用。"|  
|SQL_TRANSLATE_OPTION|一个 32 位值传递到转换.dll。|  
|SQL_TXN_ISOLATION|驱动程序允许仅 SQL_TXN_READ_COMMITTED。<br /><br /> 不支持以下 vParams:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|此 ODBC 3.0 连接属性，可在由 Microsoft 组件服务 （或 MTS，如果你使用的 Windows NT） 来协调的分布式事务中使用 Oracle ODBC 驱动程序。 它提供的接口指针*pITransaction*为作为事务*vParam*自变量。|  
|SQL_ATTR_CONNECTION_DEAD|此只读 ODBC 3.5 连接属性，可确定是否连接到 Oracle 服务器失败。 仅限; 获取无法设置。|

