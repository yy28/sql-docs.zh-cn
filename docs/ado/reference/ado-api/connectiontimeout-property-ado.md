---
title: ConnectionTimeout 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 594c96d73302b907f5bc9b2167f69c8b33047aab
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698635"
---
# <a name="connectiontimeout-property-ado"></a>ConnectionTimeout 属性 (ADO)
指示时建立的连接终止尝试并生成错误之前所等待的时间。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，该值指示，以秒为单位，多长时间等待要打开的连接。 默认值为 15。  
  
## <a name="remarks"></a>备注  
 使用**ConnectionTimeout**上的属性[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，如果从网络流量或大量服务器，请使用延迟进行必要放弃的连接尝试。 如果从时间**ConnectionTimeout**属性设置达到在连接打开之前发生错误和 ADO 取消尝试。 如果将属性设置为零，ADO 将等待无限期地打开连接。 请确保你编写的代码提供程序支持**ConnectionTimeout**功能。  
  
 **ConnectionTimeout**时该连接已关闭，只读方式打开时，属性为读/写。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [ConnectionString、 ConnectionTimeout 和 State 属性示例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和 State 属性示例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout 属性 (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
