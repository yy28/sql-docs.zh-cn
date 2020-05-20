---
title: 使用 ADO 进行 Internet 发布 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
author: rothja
ms.author: jroth
ms.openlocfilehash: b95700d30337363091815763a5e9fbf1547902e6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763058"
---
# <a name="using-ado-for-internet-publishing"></a>使用 ADO 进行 Internet 发布
[用于 Internet 发布的 OLE DB 提供程序](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)演示了使用 ADO 访问异类数据的特定示例。 虽然本部分中的示例将特定于使用 Internet 发布提供程序，但在将 ADO 用于其他提供程序的异类数据（如提供程序到电子邮件存储）时，演示的原则应类似。  
  
## <a name="urls"></a>URL  
 统一资源定位器（Url）可用作连接字符串和命令文本的替代方法，以指定数据源以及文件和目录的位置。 可以将 Url 用于现有[连接](../../../ado/reference/ado-api/connection-object-ado.md)和**记录集**对象，并使用**记录**和**流**对象。  
  
 有关如何使用 Url 的详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="record-fields"></a>记录字段  
 异类数据和同类数据之间的区别在于：对于前者，每行数据或**记录**可以具有一组不同的列或**字段**。 对于同类数据，每行都具有相同的列集。 有关特定于 Internet 发布提供程序的字段的详细信息，请参阅[记录和提供程序提供的额外字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
### <a name="appending-new-fields"></a>追加新字段  
 已增强几个 ADO 对象，使其与**Record**和**Stream**对象一起工作。  
  
-   [字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[Append](../../../ado/reference/ado-api/append-method-ado.md)方法用于创建[字段](../../../ado/reference/ado-api/field-object.md)对象并将其添加到集合，还可以指定**字段**的值。  
  
-   [Update](../../../ado/reference/ado-api/update-method.md)方法完成了向集合中添加或删除字段的操作。  
  
-   作为**Append**方法的快捷方式和替代方法，您可以通过将值分配给未定义或之前删除的字段来创建字段。  
  
 本部分包含以下主题。  
  
-   [用于 Internet 发布的 OLE DB 提供程序](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [绝对和相对 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [记录和提供程序提供的字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>另请参阅  
 [Record 对象（ADO）](../../../ado/reference/ado-api/record-object-ado.md)   
 [Stream 对象（ADO）](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 历史记录](../../../ado/guide/ado-history.md)
