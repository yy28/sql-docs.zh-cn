---
title: CommandStream 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ec65380bfea16d38f02cab0a070ab69f85d525
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919747"
---
# <a name="commandstream-property-ado"></a>CommandStream 属性 (ADO)
指示用作输入的流[命令](../../../ado/reference/ado-api/command-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回的流作为输入用于**命令**对象。 此流的格式是特定于提供程序;请参阅详细信息的提供程序的文档。 此属性是类似于[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性，用于指定的输入字符串**命令**。  
  
## <a name="remarks"></a>备注  
 **CommandStream**并**CommandText**互相排斥。 当用户设置**CommandStream**属性， **CommandText**属性将设置为空字符串 ("")。 如果用户设置**CommandText**属性， **CommandStream**属性将设置为**Nothing**。  
  
 行为**Command.Parameters.Refresh**并**Command.Prepare**方法定义提供程序。 可以刷新流中的参数值。  
  
 输入的流不是提供给其他 ADO 对象返回的源**命令**。 例如，如果[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)设置为**命令**具有作为其输入流对象**Recordset.Source**返回将继续**CommandText**属性，其中包含空字符串 ("")，而不是流内容**CommandStream**属性。  
  
 使用命令流时 (所指定的**CommandStream**)，唯一有效[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性是**adCmdText**并**adCmdUnknown**。 任何其他值将导致错误。  
  
## <a name="applies-to"></a>适用范围  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Dialect 属性](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
