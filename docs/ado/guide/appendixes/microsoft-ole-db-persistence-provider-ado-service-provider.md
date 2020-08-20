---
description: 'Microsoft OLE DB 永久性提供程序 (ADO 服务提供程序) '
title: Microsoft OLE DB 永久性提供程序 (ADO 服务提供程序) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9a1211a84bf42afdb406c085e57f5bb36f48a168
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454109"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 永久性提供程序概述
利用 Microsoft OLE DB 持久性提供程序，您可以将 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md) 对象保存到文件中，然后从文件还原该 **记录集** 对象。 将保留架构信息、数据和挂起的更改。

 您可以将 **记录集** 保存在专用高级数据表 (ADTG) 格式或 open 可扩展标记语言 (XML) 格式中。

## <a name="provider-keyword"></a>Provider 关键字
 若要调用该提供程序，请在连接字符串中指定以下关键字和值。

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>错误
 可以在应用程序中检测到此提供程序发出的以下错误。

|返回的常量|描述|
|--------------|-----------------|
|E_BADSTREAM|打开的文件的格式 (无效，格式不是 ADTG 或 XML) 。|
|E_CANTPERSISTROWSET|保存的 **记录集** 对象具有防止其被存储的特征。|

## <a name="remarks"></a>备注
 Microsoft OLE DB 永久性提供程序不公开任何动态属性。

 目前只能保存参数化分层 **记录集** 对象。

 有关永久存储 **记录集** 对象的详细信息，请参阅 [记录集持久性](../../../ado/guide/data/more-about-recordset-persistence.md)。

 当使用流打开**记录集时，** 除了**Open**方法的*Source*参数外，不应指定任何参数。

## <a name="see-also"></a>另请参阅
[Microsoft OLE DB 永久性提供程序 (ADO 服务提供程序) ](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
