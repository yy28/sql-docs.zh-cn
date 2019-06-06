---
title: Microsoft 数据整理服务用于 OLE DB （ADO 服务提供程序） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7741cc84b27991cc0831e5e28f397f46d22020a6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701216"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft 数据整理服务的 OLE DB 概述
> [!IMPORTANT]
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，应用程序应使用 XML。

 Microsoft Data Shaping 服务的 OLE DB 服务访问接口支持分层的构造 （形状）[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从数据访问接口的对象。

## <a name="provider-keyword"></a>提供程序关键字
 若要调用的 OLE DB Data Shaping 服务，请连接字符串中指定以下关键字和值。

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>动态属性
 当调用该服务提供程序时，将以下动态属性添加到[属性](../../../ado/reference/ado-api/properties-collection-ado.md)系列[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。

|动态属性名称|Description|
|---------------------------|-----------------|
|**唯一调整形状名称**|指示是否**记录集**具有重复值的对象及其**重新调整形状名称**允许使用属性。 如果此动态属性是 **，则返回 True**和一个新**记录集**创建具有相同的用户指定调整形状名称与现有**记录集**，然后新**记录集**修改对象的形状名称使其成为唯一。 如果此属性为**False**和一个新**记录集**创建具有相同的用户指定调整形状名称与现有**记录集**，这两个**记录集**对象将具有相同的调整形状名称。 因此，既不**记录集**考虑，只要这两个记录集存在。<br /><br /> 该属性的默认值是**False**。|
|**数据提供程序**|指示将提供的形状的行的提供程序的名称。 如果提供程序不会用于提供行，此值可以为 NONE。|

 此外可以通过指定其名称为连接字符串中的关键字设置可写的动态属性。 例如，在 Microsoft Visual Basic 中，设置**数据提供程序**动态属性设置为"MSDASQL"通过指定：

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 此外可以设置或通过指定其名称为索引来检索动态属性[属性](../../../ado/reference/ado-api/properties-collection-ado.md)属性。 例如，下面的代码示例获取并列显的当前值**数据提供程序**动态属性，然后设置新值，如果 cn。数据提供程序已设置为"MSDataShape"(直接或间接通过连接字符串) 和未打开连接：

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  动态属性**数据提供程序**，可以是仅设置上未打开**连接**对象。 打开连接时，一旦**数据提供程序**属性将变为只读。

 有关数据调整的详细信息，请参阅[数据整理](../../../ado/guide/data/data-shaping-overview.md)。

## <a name="see-also"></a>请参阅
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
