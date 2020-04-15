---
title: 连接选项 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25cfe2a897b0c312f91cd0c1e41ad6fa11725ab8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281307"
---
# <a name="connect-options"></a>连接选项
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 这些选项允许自定义应用程序中的数据库连接。  
  
|连接选项|说明|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|如果选择SQL_AUTOCOMMIT_OFF，则应用程序必须显式提交或回滚[SQLTransact 的](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)事务。|  
|SQL_ODBC_CURSORS|此连接属性在驱动程序管理器中实现。|  
|SQL_OPT_TRACE|此连接属性在驱动程序管理器中实现。|  
|SQL_OPT_TRACEFILE|此连接属性在驱动程序管理器中实现。|  
|SQL_TRANSLATE_DLL|返回错误："驱动程序无法。|  
|SQL_TRANSLATE_OPTION|传递给翻译 .dll 的 32 位值。|  
|SQL_TXN_ISOLATION|驱动程序只允许SQL_TXN_READ_COMMITTED。<br /><br /> 不支持以下 vParams：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|此 ODBC 3.0 连接属性允许您在 Microsoft 组件服务（如果使用 Windows NT）协调的分布式事务中使用 Oracle 的 ODBC 驱动程序。 它提供接口指针*pI交易*到事务作为*vParam*参数。|  
|SQL_ATTR_CONNECTION_DEAD|此只读 ODBC 3.5 连接属性允许您确定与 Oracle 服务器的连接是否失败。 只获取;无法设置。|
