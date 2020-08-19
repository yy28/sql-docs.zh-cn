---
description: 连接选项
title: 连接选项 |Microsoft Docs
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
ms.openlocfilehash: 22326ca650f575c6a4f0503093306d8b68581475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483680"
---
# <a name="connect-options"></a>连接选项
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 这些选项允许自定义应用程序中的数据库连接。  
  
|连接选项|说明|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|如果选择 SQL_AUTOCOMMIT_OFF，你的应用程序必须通过 [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)显式提交或回滚事务。|  
|SQL_ODBC_CURSORS|此连接属性是在驱动程序管理器中实现的。|  
|SQL_OPT_TRACE|此连接属性是在驱动程序管理器中实现的。|  
|SQL_OPT_TRACEFILE|此连接属性是在驱动程序管理器中实现的。|  
|SQL_TRANSLATE_DLL|返回错误： "驱动程序不支持"。|  
|SQL_TRANSLATE_OPTION|传递给转换 .dll 的32位值。|  
|SQL_TXN_ISOLATION|驱动程序仅允许 SQL_TXN_READ_COMMITTED。<br /><br /> 不支持以下 vParams：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|如果使用的是 Windows NT) ，使用此 ODBC 3.0 连接属性可以在由 Microsoft 组件服务 (或 MTS 协调的分布式事务中使用适用于 Oracle 的 ODBC 驱动程序。 它提供指向事务的接口指针 *pITransaction* 作为 *vParam* 参数。|  
|SQL_ATTR_CONNECTION_DEAD|此只读 ODBC 3.5 连接属性允许您确定到 Oracle 服务器的连接是否失败。 仅获取;无法设置。|
