---
description: IndexNulls 属性 (ADOX)
title: IndexNulls 属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Index::get_IndexNulls
- _Index::GetIndexNulls
- _Index::put_IndexNulls
- _Index::PutIndexNulls
- _Index::IndexNulls
helpviewer_keywords:
- IndexNulls property [ADOX]
ms.assetid: 313b0bf7-3f37-4823-8fca-bd9c80e078a7
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b71e3298c18b10fa34615e3382d561f454b5eb4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770166"
---
# <a name="indexnulls-property-adox"></a>IndexNulls 属性 (ADOX)
指示在其索引字段中具有 null 值的记录是否具有索引条目。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回一个 [AllowNullsEnum](./allownullsenum.md) 值。 默认值为 **adIndexNullsDisallow**。  
  
## <a name="remarks"></a>备注  
 对于已追加到集合的 [索引](./index-object-adox.md) 对象，此属性是只读的。  
  
## <a name="applies-to"></a>适用于  
 [索引对象 (ADOX)](./index-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [IndexNulls 属性示例 (VB)](./indexnulls-property-example-vb.md)