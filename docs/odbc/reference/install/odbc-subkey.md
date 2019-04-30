---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee7cf624e7c118a5d9ef36738c810aecc4ec5684
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281012"
---
# <a name="odbc-subkey"></a>ODBC 子项
ODBC 子项下的值指定 ODBC 跟踪选项。 通过显示 ODBC 数据源管理器对话框的跟踪选项卡来设置这些选项**SQLManageDataSources**。 ODBC 子项本身是可选的。 这些值的格式为下表中所示。  
  
|“属性”|数据类型|数据|  
|----------|---------------|----------|  
|跟踪|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-path*|  
  
 值采用下表中描述的含义。  
  
|ReplTest1|含义|  
|-----------|-------------|  
|跟踪|如果跟踪值设置为 1 应用程序调用**SQLAllocHandle** SQL_HANDLE_ENV 选项后，调用应用程序启用跟踪。<br /><br /> 如果跟踪关键字设置为 0 中，当应用程序调用**SQLAllocHandle** SQL_HANDLE_ENV 选项后，调用应用程序禁用跟踪。 这是默认值。<br /><br /> 应用程序可以启用或禁用跟踪与 SQL_ATTR_TRACE 连接属性。 但是，这样做因此不会更改此值的数据。|  
|TraceFile|如果启用了跟踪，驱动程序管理器将写入到 TraceFile 值所指定的跟踪文件。<br /><br /> 如果指定不跟踪文件，则驱动程序管理器将写入到当前驱动器上的 Sql.log 文件。 这是默认值。<br /><br /> 跟踪应仅用于单个应用程序，或每个应用程序应指定一个不同的跟踪文件。 否则，两个或多个应用程序将尝试打开相同的跟踪文件在同一时间，从而导致错误。<br /><br /> 应用程序可以使用 SQL_ATTR_TRACEFILE 连接属性指定新的跟踪文件。 但是，这样做因此不会更改此值的数据。|  
  
 例如，假设启用了跟踪和跟踪文件是 C:\Odbc.log。 ODBC 子项下的值将按如下所示：  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
