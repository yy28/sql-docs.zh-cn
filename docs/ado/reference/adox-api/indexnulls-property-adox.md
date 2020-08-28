---
description: IndexNulls 属性 (ADOX)
title: IndexNulls 属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 055b873866758c4aede2a3f6364eb99036159427
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984148"
---
# <a name="indexnulls-property-adox"></a>IndexNulls 属性 (ADOX)
指示在其索引字段中具有 null 值的记录是否具有索引条目。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置并返回一个 [AllowNullsEnum](./allownullsenum.md) 值。 默认值为 **adIndexNullsDisallow**。  
  
## <a name="remarks"></a>注解  
 对于已追加到集合的 [索引](./index-object-adox.md) 对象，此属性是只读的。  
  
## <a name="applies-to"></a>适用于  
 [索引对象 (ADOX)](./index-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [IndexNulls 属性示例 (VB)](./indexnulls-property-example-vb.md)