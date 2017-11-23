---
title: "ConnectionTimeout 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Connection15::ConnectionTimeout
helpviewer_keywords: ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 17572bfd4ef1de5fa20246f88c8a0187409bbfd4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="connectiontimeout-property-ado"></a>ConnectionTimeout 属性 (ADO)
指示多长时间来建立的连接在终止尝试并生成错误之前，请稍候。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**长**值，该值指示，以秒为单位，多长时间等待要打开的连接。 默认值为 15。  
  
## <a name="remarks"></a>注释  
 使用**ConnectionTimeout**属性[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象如果从网络流量或大量服务器，请使用延迟使其成为需放弃的连接尝试。 如果从时间**ConnectionTimeout** ADO 取消尝试和设置的属性经过该连接，在打开之前发生错误。 如果将属性设置为零，ADO 将等到无限期地打开连接。 请确保你编写的代码提供程序支持**ConnectionTimeout**功能。  
  
 **ConnectionTimeout**属性为读/写，当连接已关闭，并且只读打开时。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ConnectionString、 ConnectionTimeout，以及状态属性示例 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、 ConnectionTimeout 和状态属性示例 （VC + +）](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout 属性 (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
