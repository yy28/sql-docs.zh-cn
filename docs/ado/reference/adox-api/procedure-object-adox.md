---
title: Procedure 对象（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedure
helpviewer_keywords:
- Procedure object [ADOX]
ms.assetid: 927bcf3e-32f5-4a80-98d3-600779f0732e
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a56088e47a9f794f1862ef87bf142a8d3ab12c4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763688"
---
# <a name="procedure-object-adox"></a>过程对象 (ADOX)
表示存储过程。 与 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)对象结合使用时，可以使用**Procedure**对象添加、删除或修改存储过程。  
  
## <a name="remarks"></a>备注  
 使用**Procedure**对象，您可以创建一个存储过程，而无需知道或使用该提供程序的 "create Procedure" 语法。  
  
 使用**过程**对象的属性，可以：  
  
-   标识具有[Name](../../../ado/reference/adox-api/name-property-adox.md)属性的过程。  
  
-   指定可用于使用[Command](../../../ado/reference/adox-api/command-property-adox.md)属性创建或执行该过程的 ADO**命令**对象。  
  
-   返回具有[DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md)和[DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md)属性的日期信息。  
  
 本部分包含以下主题。  
  
-   [过程对象属性、方法和事件](../../../ado/reference/adox-api/procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [Command 和 CommandText 属性示例（VB）](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Parameters 集合、Command 属性示例（VB）](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [过程 Append 方法示例（VB）](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [过程 Delete 方法示例（VB）](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
