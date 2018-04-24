---
title: CommandStream 属性 (ADO) |Microsoft 文档
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
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f720cc4ab3b388f974d34e23690b8aef91c20ba3
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="commandstream-property-ado"></a>CommandStream 属性 (ADO)
指示用作输入的流[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回用作输入的流**命令**对象。 此流的格式是特定于提供程序;请参阅详细信息的提供程序的文档。 此属性是类似于[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性，用于指定的输入的字符串**命令**。  
  
## <a name="remarks"></a>注释  
 **CommandStream**和**CommandText**是互相排斥。 当用户设置**CommandStream**属性， **CommandText**属性将设置为空字符串 ("")。 如果用户设置**CommandText**属性， **CommandStream**属性将设置为**执行任何操作**。  
  
 行为**Command.Parameters.Refresh**和**Command.Prepare**方法定义提供程序。 无法刷新流中的参数值。  
  
 输入的流不是提供给返回的源其他 ADO 对象**命令**。 例如，如果[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)设置为**命令**具有作为其输入流的对象**Recordset.Source**继续返回**CommandText**属性，其中包含一个空字符串 ("")，而不是流内容的**CommandStream**属性。  
  
 使用命令流时 (所指定的**CommandStream**)，仅有的有效[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性**adCmdText**和**adCmdUnknown**。 任何其他值将导致错误。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [方言属性](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
