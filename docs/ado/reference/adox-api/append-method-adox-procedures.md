---
title: Append 方法（ADOX 过程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: rothja
ms.author: jroth
ms.openlocfilehash: c703843781558839a3f4f275a8427f69770a8690
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764068"
---
# <a name="append-method-adox-procedures"></a>Append 方法（ADOX 过程）
将新[过程](../../../ado/reference/adox-api/procedure-object-adox.md)对象添加到[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>参数  
 *Name*  
 一个**字符串**值，该值指定要创建并追加的过程的名称。  
  
 *命令*  
 一个 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，表示要创建和追加的过程。  
  
## <a name="remarks"></a>备注  
 使用**Command**对象中指定的名称和属性在数据源中创建一个新过程。  
  
 如果用户指定的命令文本表示视图而不是过程，则行为取决于所使用的提供程序。 如果提供程序不支持保留命令，则**Append**将会失败。  
  
> [!NOTE]
>  使用适用于 Microsoft Jet 的 OLE DB 提供程序时 **，过程**集合**Append**方法将允许您在*Command*参数中指定**视图**，而不是**过程**。 **视图**将添加到数据源，并将添加到 "**过程**" 集合中。 **追加**后，如果刷新了 "**过程**" 和 "**视图**" 集合，则该**视图**将不再出现在 "**过程**" 集合中，并将显示在 "**视图**" 集合中。  
  
## <a name="applies-to"></a>应用于  
 [过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [过程 Append 方法示例（VB）](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append 方法（ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
