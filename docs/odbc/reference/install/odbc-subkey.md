---
title: ODBC 子键 |微软文档
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
ms.openlocfilehash: 96e9a5f4c3cdac5097686528d3c089d9ec5826f7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287437"
---
# <a name="odbc-subkey"></a>ODBC 子项
ODBC 子键下的值指定 ODBC 跟踪选项。 这些选项通过**SQLManageDataSource**显示的 ODBC 数据源管理员对话框的"跟踪"选项卡进行设置。 ODBC 子密钥本身是可选的。 这些值的格式如下表所示。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|跟踪|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*跟踪文件路径*|  
  
 这些值具有下表中描述的含义。  
  
|“值”|含义|  
|-----------|-------------|  
|跟踪|如果使用SQL_HANDLE_ENV选项调用**SQLAllocHandle**时跟踪值设置为 1，则为调用应用程序启用跟踪。<br /><br /> 如果跟踪关键字在应用程序使用SQL_HANDLE_ENV选项调用**SQLAllocHandle**时设置为 0，则禁用调用应用程序的跟踪。 这是默认值。<br /><br /> 应用程序可以使用SQL_ATTR_TRACE连接属性启用或禁用跟踪。 但是，这样做不会更改此值的数据。|  
|TraceFile|如果启用了跟踪，驱动程序管理器将写入跟踪文件值指定的跟踪文件。<br /><br /> 如果未指定跟踪文件，驱动程序管理器将写入当前驱动器上的 Sql.log 文件。 这是默认值。<br /><br /> 跟踪应仅用于单个应用程序，或者每个应用程序应指定不同的跟踪文件。 否则，两个或多个应用程序将尝试同时打开同一跟踪文件，从而导致错误。<br /><br /> 应用程序可以使用SQL_ATTR_TRACEFILE连接属性指定新的跟踪文件。 但是，这样做不会更改此值的数据。|  
  
 例如，假设已启用跟踪，并且跟踪文件为 C：_Odbc.log。 ODBC 子键下的值如下所示：  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
