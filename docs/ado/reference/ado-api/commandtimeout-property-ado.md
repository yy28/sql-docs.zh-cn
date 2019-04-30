---
title: CommandTimeout 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5bb74384e043130ccfe4c3399b363b25d40737c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315951"
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout 属性 (ADO)
指示在终止尝试并生成错误之前执行命令时，请等待的时间。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，该值指示，以秒为单位，多长时间等待要执行的命令。 默认值为 30。  
  
## <a name="remarks"></a>备注  
 使用**CommandTimeout**上的属性[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象或[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，以允许取消[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法由于网络流量或大量服务器，请使用从延迟调用。 如果在间隔中设置**CommandTimeout**前该命令完成执行时，出现错误和 ADO 取消的命令经过的属性。 如果将属性设置为零，ADO 将执行完成之前无限期等待。 请确保你编写的代码的支持的提供程序和数据源**CommandTimeout**功能。  
  
 **CommandTimeout**上设置**连接**对象不起任何作用**CommandTimeout**上设置**命令**对象上相同**连接**; 即**命令**对象的**CommandTimeout**属性不会继承的值**连接**对象的**CommandTimeout**值。  
  
 上**连接**对象， **CommandTimeout**后的属性保持为读/写**连接**打开。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 （VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、 CommandText、 CommandTimeout、 CommandType、 大小和方向属性示例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout 属性 (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
