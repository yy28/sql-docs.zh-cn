---
title: "Append 方法 （ADOX 过程） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cdf43784501659e3fd4da883ddeac33439a30719
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-adox-procedures"></a>Append 方法 （ADOX 过程）
添加新[过程](../../../ado/reference/adox-api/procedure-object-adox.md)对象传递给[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
 A**字符串**值，该值指定要创建并追加过程的名称。  
  
 *Command*  
 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)对象，表示要创建并追加的过程。  
  
## <a name="remarks"></a>注释  
 在具有名称和特性中指定的数据源中创建新的过程**命令**对象。  
  
 如果用户指定的命令文本表示视图而不是一个过程，该行为不依赖于正在使用的提供程序。 **追加**如果提供程序不支持保留命令将失败。  
  
> [!NOTE]
>  使用用于 Microsoft Jet 的 OLE DB 提供程序时**过程**集合**追加**方法将允许你指定**视图**而不是**过程**中*命令*参数。 **视图**将添加到数据源，将添加到**过程**集合。 后**追加**，如果**过程**和**视图**刷新集合，**视图**将不再在**过程**集合并将显示在**视图**集合。  
  
## <a name="applies-to"></a>适用范围  
 [过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [过程追加方法示例 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 组）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 用户）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)
