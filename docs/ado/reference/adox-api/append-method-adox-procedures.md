---
title: Append 方法 （ADOX 过程） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 348b2876e4293ad912383859ace47e462da31bcf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707954"
---
# <a name="append-method-adox-procedures"></a>Append 方法（ADOX 过程）
添加一个新[过程](../../../ado/reference/adox-api/procedure-object-adox.md)对象传递给[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 一个**字符串**值，该值指定要创建并追加过程的名称。  
  
 *Command*  
 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，表示要创建并追加的过程。  
  
## <a name="remarks"></a>备注  
 在属性中指定的名称与数据源中创建一个新的过程**命令**对象。  
  
 如果用户指定的命令文本表示视图而不是一个过程，则行为将取决于正在使用的提供程序。 **追加**如果提供程序不支持保留命令将失败。  
  
> [!NOTE]
>  当使用 OLE DB Provider for Microsoft Jet**过程**集合**追加**方法将允许您指定**视图**而非**过程**中*命令*参数。 **视图**将添加到数据源，将添加到**过程**集合。 之后**追加**，则**过程**并**视图**集合会进行刷新，**视图**将不再在**过程**集合，将显示在**视图**集合。  
  
## <a name="applies-to"></a>适用范围  
 [过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [过程 Append 方法示例 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 项）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
