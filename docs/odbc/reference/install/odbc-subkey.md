---
title: ODBC 子项 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4f7f404eedb8b72f744c882cc69edf2ebc0d515
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-subkey"></a>ODBC 子项
ODBC 子项下的值指定 ODBC 跟踪选项。 通过 ODBC 数据源管理器中显示的对话框的跟踪选项卡来设置这些选项**SQLManageDataSources**。 ODBC 子项本身是可选的。 下表中所示，将为这些值的格式。  
  
|名称|数据类型|Data|  
|----------|---------------|----------|  
|跟踪|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile 路径*|  
  
 值具有下表中描述的含义。  
  
|“值”|含义|  
|-----------|-------------|  
|跟踪|如果跟踪值设置为 1 时应用程序调用**SQLAllocHandle**使用 SQL_HANDLE_ENV 选项中，对调用应用程序启用跟踪。<br /><br /> 如果跟踪关键字设置为 0 时应用程序调用**SQLAllocHandle** SQL_HANDLE_ENV 选项后，调用应用程序禁用跟踪。 这是默认值。<br /><br /> 应用程序可以启用或禁用与 SQL_ATTR_TRACE 连接属性的跟踪。 但是，这样做因此不会更改此值的数据。|  
|TraceFile|如果启用了跟踪，驱动程序管理器将写入 TraceFile 值指定的跟踪文件。<br /><br /> 如果不指定任何跟踪文件，则驱动程序管理器将写入当前的驱动器上的 Sql.log 文件。 这是默认值。<br /><br /> 跟踪应仅用于单个应用程序，或每个应用程序应指定一个不同的跟踪文件。 否则，两个或多个应用程序将尝试打开相同的跟踪文件在同一时间，从而导致错误。<br /><br /> 应用程序可以使用 SQL_ATTR_TRACEFILE 连接属性指定新的跟踪文件。 但是，这样做因此不会更改此值的数据。|  
  
 例如，假设跟踪处于启用状态，跟踪文件是 C:\Odbc.log。 ODBC 子项下的值将如下所示：  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
