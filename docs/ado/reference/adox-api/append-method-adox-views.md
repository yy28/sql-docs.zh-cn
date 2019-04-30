---
title: Append 方法 （ADOX 视图） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 584c3d0144197425b307f2d4a04bd8a09f27a36c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184217"
---
# <a name="append-method-adox-views"></a>Append 方法（ADOX 视图）
创建一个新[视图](../../../ado/reference/adox-api/view-object-adox.md)对象，并将其附加到[视图](../../../ado/reference/adox-api/views-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 一个**字符串**值，该值指定要创建的视图的名称。  
  
 *Command*  
 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，表示要创建的视图。  
  
## <a name="remarks"></a>备注  
 在属性中指定的名称与数据源中创建新的视图**命令**对象。  
  
 如果用户指定的命令文本表示过程而不是一个视图，则行为将取决于提供程序。 **追加**如果提供程序不支持保留命令将失败。  
  
> [!NOTE]
>  当使用 OLE DB Provider for Microsoft Jet**视图**集合**追加**方法将允许您指定**过程**而非**视图**中*命令*参数。 **过程**将添加到数据源，将添加到**视图**集合。 之后**追加**，则**过程**并**视图**集合会进行刷新，**过程**将不再在**视图**集合，将显示在**过程**集合。  
  
## <a name="applies-to"></a>适用范围  
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [视图 Append 方法示例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 项）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)
