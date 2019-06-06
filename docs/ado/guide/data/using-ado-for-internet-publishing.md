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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ac7922dda2d486f4783d1230296dc89b81cb4fe3
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718605"
---
# <a name="using-ado-for-internet-publishing"></a>使用 ADO 进行 Internet 发布
[用于 Internet 发布的 OLE DB 提供程序](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)显示了访问与 ADO 一起异类数据的特定示例。 尽管本部分中的示例将特定于使用 Internet 发布提供程序，与其他异类数据，如电子邮件存储区的提供者的提供程序使用 ADO 时应类似演示的原则。  
  
## <a name="urls"></a>URL  
 统一资源定位器 (Url) 可以作为连接字符串和命令文本的替代方法，用于指定数据源和文件和目录的位置。 可以使用与现有的 Url[连接](../../../ado/reference/ado-api/connection-object-ado.md)并**记录集**对象且**记录**并**Stream**对象。  
  
 有关如何使用 Url 的详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="record-fields"></a>记录字段  
 异类数据与同类数据之间的差别是，对于前者，每行数据，或**记录**，可以有一组不同的列，或**字段**。 同类数据，对于每个行包含相同的列集。 有关特定于 Internet 发布提供程序的字段的详细信息，请参阅[记录和提供程序提供额外字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
### <a name="appending-new-fields"></a>追加新的字段  
 ADO 的多个对象已得到增强，一起使用**记录**并**Stream**对象。  
  
-   [字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[追加](../../../ado/reference/ado-api/append-method-ado.md)方法，它会创建并添加[字段](../../../ado/reference/ado-api/field-object.md)到集合对象，还可以指定的值**字段**.  
  
-   [更新](../../../ado/reference/ado-api/update-method.md)方法完成的添加或删除的字段集合。  
  
-   作为快捷方式和替代方法**追加**方法，您可以通过将值分配给一个未定义或以前已删除的字段创建字段。  
  
 本部分包含以下主题。  
  
-   [用于 Internet 发布的 OLE DB 提供程序](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [绝对和相对 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [记录和提供程序提供的字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>请参阅  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Stream 对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 历史记录](../../../ado/guide/ado-history.md)
