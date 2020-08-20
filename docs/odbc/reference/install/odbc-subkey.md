---
description: ODBC 子项
title: ODBC 子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec27b40e196f5277307b9a299dd865a1604dc0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499722"
---
# <a name="odbc-subkey"></a>ODBC 子项
ODBC 子项下的值指定 ODBC 跟踪选项。 通过 **SQLManageDataSources**显示的 "ODBC 数据源管理器" 对话框中的 "跟踪" 选项卡设置这些选项。 ODBC 子项本身是可选的。 这些值的格式如下表中所示。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|跟踪|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-路径*|  
  
 这些值的含义如下表所述。  
  
|值|含义|  
|-----------|-------------|  
|跟踪|当应用程序使用 SQL_HANDLE_ENV 选项调用 **SQLAllocHandle** 时，如果跟踪值设置为1，则为调用应用程序启用跟踪。<br /><br /> 当应用程序使用 SQL_HANDLE_ENV 选项调用 **SQLAllocHandle** 时，如果 Trace 关键字设置为0，则对调用应用程序禁用跟踪。 这是默认值。<br /><br /> 应用程序可以使用 SQL_ATTR_TRACE 连接属性启用或禁用跟踪。 但这样做不会更改此值的数据。|  
|TraceFile|如果启用跟踪，驱动程序管理器会写入由 TraceFile 值指定的跟踪文件。<br /><br /> 如果未指定任何跟踪文件，则驱动程序管理器将写入当前驱动器上的 Sql .log 文件。 这是默认值。<br /><br /> 跟踪只应用于单个应用程序，或每个应用程序应指定一个不同的跟踪文件。 否则，两个或多个应用程序将尝试同时打开同一跟踪文件，从而导致错误。<br /><br /> 应用程序可以使用 SQL_ATTR_TRACEFILE 连接属性指定新的跟踪文件。 但这样做不会更改此值的数据。|  
  
 例如，假设已启用跟踪并且跟踪文件为 C:\Odbc.log。 ODBC 子项下的值如下所示：  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
