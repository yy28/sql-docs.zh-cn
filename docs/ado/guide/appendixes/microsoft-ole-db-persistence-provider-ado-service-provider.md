---
title: "Microsoft OLE DB 永久性提供程序 （ADO 服务提供商） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 846abf657a2cce58fec6dca65f80691f14cb52a4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 持久性提供程序概述
Microsoft OLE DB 永久性提供程序使你可以保存[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象为文件，并在以后还原，**记录集**文件中的对象。 架构信息、 数据和挂起的更改将被保留。

 可以保存**记录集**专有的高级数据表克 (ADTG) 格式或打开的可扩展标记语言 (XML) 格式中。

## <a name="provider-keyword"></a>提供程序关键字
 若要调用此提供程序，请在连接字符串中指定以下关键字和值。

```
"Provider=MSPersist"
```

## <a name="errors"></a>错误
 在你的应用程序中，可以检测到此提供程序发出了以下错误。

|常量|Description|
|--------------|-----------------|
|E_BADSTREAM|打开的文件不是有效的格式 （即的格式不 ADTG 或 XML）。|
|E_CANTPERSISTROWSET|**记录集**保存对象具有阻止存储的特征。|

## <a name="remarks"></a>Remarks
 Microsoft OLE DB 永久性提供程序公开任何动态属性。

 目前，只有参数化分层**记录集**无法保存对象。

 有关详细信息，有关永久存储**记录集**对象，请参阅[记录集持久性](../../../ado/guide/data/more-about-recordset-persistence.md)。

 当流用于打开**记录集，**不应而不指定任何参数*源*参数**打开**方法。

## <a name="see-also"></a>另请参阅
[Microsoft OLE DB 永久性提供程序 （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
