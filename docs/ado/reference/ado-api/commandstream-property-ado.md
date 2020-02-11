---
title: CommandStream 属性（ADO） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919747"
---
# <a name="commandstream-property-ado"></a>CommandStream 属性 (ADO)
指示用作[命令](../../../ado/reference/ado-api/command-object-ado.md)对象的输入的流。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回用作**命令**对象输入的流。 此流的格式特定于提供程序;有关详细信息，请参阅提供程序的文档。 此属性类似于[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)属性，该属性用于指定**命令**输入的字符串。  
  
## <a name="remarks"></a>备注  
 **CommandStream**和**CommandText**互相排斥。 当用户设置**CommandStream**属性时， **CommandText**属性将设置为空字符串（""）。 如果用户设置**CommandText**属性，则**CommandStream**属性将设置为**Nothing**。  
  
 命令的行为。**参数**和**命令。 Prepare**方法由提供程序定义。 流中的参数值无法刷新。  
  
 输入流不能用于返回**命令**源的其他 ADO 对象。 例如，如果将[记录](../../../ado/reference/ado-api/recordset-object-ado.md)集的[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)设置为将流作为其输入的**命令**对象，则**记录集。源**继续返回**CommandText**属性，该属性包含空字符串（""），而不是**CommandStream**属性的流内容。  
  
 使用命令流（由**CommandStream**指定）时， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性唯一的有效[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值为**adCmdText**和**adCmdUnknown**。 其他任何值会导致错误。  
  
## <a name="applies-to"></a>应用于  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CommandText 属性（ADO）](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [方言属性](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
