---
title: 用于 Internet 发布的 ADO |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 642f4eb6f145b7488766688c758660521c74fa8f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="using-ado-for-internet-publishing"></a>ADO 用于 Internet 发布
[OLE DB Provider for Internet 发布](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)显示访问用 ADO 异类数据的特定示例。 尽管此部分中的示例将特定于使用 Internet 发布提供程序，与其他提供程序与异类数据，如到电子邮件存储区提供程序一起使用 ADO 时应类似演示的原则。  
  
## <a name="urls"></a>URL  
 统一资源定位器 (Url) 可以作为连接字符串和命令文本的替代方法，用于指定数据源和文件和目录的位置。 可以使用的 Url 与现有[连接](../../../ado/reference/ado-api/connection-object-ado.md)和**记录集**对象与**记录**和**流**对象。  
  
 有关如何使用 Url 的详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="record-fields"></a>记录字段  
 异类数据和同类数据之间的差别在于，前者，每行数据，或**记录**，可以具有一组不同的列，或**字段**。 同类数据，对于每个行具有相同的列集。 有关特定于 Internet 发布提供程序的字段的详细信息，请参阅[记录和提供程序提供额外字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
### <a name="appending-new-fields"></a>追加新字段  
 几个 ADO 对象已增强，从而一起使用**记录**和**流**对象。  
  
-   [字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[追加](../../../ado/reference/ado-api/append-method-ado.md)方法，它创建并添加[字段](../../../ado/reference/ado-api/field-object.md)到集合对象，还可以指定的值**字段**.  
  
-   [更新](../../../ado/reference/ado-api/update-method.md)方法完成的添加或删除到集合的字段。  
  
-   作为快捷方式和替代**追加**方法中，你可以通过将值分配给未定义的或以前已删除的字段创建字段。  
  
 本部分包含以下主题。  
  
-   [用于 Internet 发布的 OLE DB 提供程序](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [绝对和相对 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [记录和提供程序提供的字段](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>另请参阅  
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 历史记录](../../../ado/guide/ado-history.md)
