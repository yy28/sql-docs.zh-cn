---
title: Microsoft OLE DB 永久性提供程序 （ADO 服务提供程序） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2550e36f977be13e10865d4bd238c8508c542091
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128510"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 暂留提供程序概述
Microsoft OLE DB 永久性提供程序使您可以保存[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象到文件中，并在以后还原该**记录集**文件中的对象。 架构信息和数据，而挂起的更改将保留。

 您可以保存**记录集**中专用的高级数据表元语法 (ADTG) 格式或开放的可扩展标记语言 (XML) 格式。

## <a name="provider-keyword"></a>提供程序关键字
 若要调用此提供程序，请连接字符串中指定以下关键字和值。

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>错误
 可以在应用程序中检测到此提供程序颁发以下错误。

|常量|Description|
|--------------|-----------------|
|E_BADSTREAM|打开的文件不具有有效的格式 （即，格式不是 ADTG 或 XML）。|
|E_CANTPERSISTROWSET|**记录集**保存对象具有防止将其存储的特征。|

## <a name="remarks"></a>备注
 Microsoft OLE DB 永久性提供程序公开任何动态属性。

 目前，仅参数化分层**记录集**无法保存对象。

 有关永久存储的详细信息**记录集**对象，请参阅[记录集暂留](../../../ado/guide/data/more-about-recordset-persistence.md)。

 当使用流来打开**记录集，** 不应而不指定任何参数*源*参数**打开**方法。

## <a name="see-also"></a>请参阅
[Microsoft OLE DB 永久性提供程序 （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
