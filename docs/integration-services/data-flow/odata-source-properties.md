---
title: "OData 源属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 64e297a37c3b6449551968b5788f8c2c0ddd4ab6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/23/2017

---
# <a name="odata-source-properties"></a>OData 源属性
当您右键单击**OData 源**数据流然后单击**属性**，请参阅属性**OData 源**中为组件**属性**窗口。  

## <a name="properties"></a>属性 
|属性|Description|  
|-|-|  
|CollectionName|要从 OData 服务检索的集合的名称。 **“CollectionName”** 属性在 **UseResourcePath** 为 False 时使用。<br /><br /> 此属性是 expressionable，这样就可以在运行时将值设置。 但是，如果集合的元数据与在设计时存在的元数据不匹配，会发生验证错误，导致数据流执行失败。|  
|DefaultStringLength|此值为没有最大长度的字符串列指定默认长度。<br /><br /> **默认值：** 4000|  
|Query|OData 查询参数。 此属性是 expressionable，可以在运行时设置。|  
|ResourcePath|在需要指定完整资源路径（而不仅仅是选择集合名称）时使用此属性。 此属性在 **UseResourcePath** 为 True 时使用。|  
|UseResourcePath|设置为 True 时， **ResourcePath** 值追加到基 URL 以确定 OData 馈送位置。 设置为 False 时 ，使用 **CollectionName** 值。<br /><br /> **默认值：** False|  
  
## <a name="see-also"></a>另请参阅
[OData 源](odata-source.md)

