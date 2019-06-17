---
title: ActiveConnection 属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6ad7cdfdfc3c08175faf0584f2ae5069fcd39acb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719019"
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection 属性 (ADO MD)
指示对哪些 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象当前的单元集或当前所属的编录。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**Variant** ，其中包含定义连接字符串或**连接**对象。 默认值为空。  
  
## <a name="remarks"></a>备注  
 可以将此属性设置为有效的 ADO**连接**对象或到有效的连接字符串。 当此属性设置为连接字符串时，该提供程序创建一个新**连接**对象使用此定义，并打开的连接。  
  
 如果您使用*ActiveConnection*的参数[打开](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法以打开[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)对象， **ActiveConnection**属性将继承自变量的值。  
  
 设置**ActiveConnection**的属性[目录](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)对象传递给**Nothing**释放相关联的数据，包括中的数据[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合和任何相关[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)，并且[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象。 关闭**连接**对象，用于打开**目录**具有相同的效果与设置**ActiveConnection**属性设置为**Nothing**.  
  
 更改引用的连接的默认数据库**ActiveConnection**的属性**目录**对象使无效的内容**目录**。  
  
 如果尝试进行更改，将会出错**ActiveConnection**属性的一种开放**单元集**对象。  
  
> [!NOTE]
>  在 Visual Basic 中，请务必使用**设置**关键字设置时**ActiveConnection**属性设置为**连接**对象。 如果省略**设置**关键字，将实际设置**ActiveConnection**属性等于**连接**对象的默认属性**ConnectionString**。 这些代码将正常工作;但是，您将创建数据源，这可能产生负面的性能影响的其他连接。  
  
 当使用 MSOLAP 数据访问接口，在服务器名称的连接字符串中设置数据源并从数据源设置为目录的名称的初始目录。 若要连接到多维数据集文件从服务器断开连接，请将位置设置为的完整路径。CUB 文件。 在任一情况下，将设置提供程序提供程序名称。 例如，以下字符串使用 MSOLAP 访问接口连接到名为的服务器上名为 Bobs 视频应用商店目录**Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 下面的字符串连接到本地多维数据集文件的位置 C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub:  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[目录对象 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[单元集对象 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>请参阅  
 [单元集示例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open 方法 (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
