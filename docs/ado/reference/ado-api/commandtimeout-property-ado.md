---
title: CommandTimeout 属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9a1e5d670917520db70812a0eb17141c643b4e8d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout 属性 (ADO)
指示在终止尝试并生成错误之前执行命令时所等待的时间。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，该值指示，以秒为单位，多长时间等待要执行的命令。 默认值为 30。  
  
## <a name="remarks"></a>注释  
 使用**CommandTimeout**属性[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象或[命令](../../../ado/reference/ado-api/command-object-ado.md)对象以允许取消[执行](../../../ado/reference/ado-api/execute-method-ado-command.md)方法调用时，由从网络流量或大量服务器使用的延迟。 如果在中设置的间隔**CommandTimeout**之前该命令完成执行，就会出错并 ADO 取消的命令经过的属性。 如果将属性设置为零，ADO 将等待无限期地执行完成。 请确保你编写的代码的支持的提供程序和数据源**CommandTimeout**功能。  
  
 **CommandTimeout**上设置**连接**对象不起任何作用**CommandTimeout**上设置**命令**对象上同一**连接**; 即，**命令**对象的**CommandTimeout**属性不会继承的值**连接**对象的**CommandTimeout**值。  
  
 上**连接**对象， **CommandTimeout**后的属性保持为读/写**连接**打开。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout 属性 (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
