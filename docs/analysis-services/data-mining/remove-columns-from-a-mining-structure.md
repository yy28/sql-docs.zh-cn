---
title: 从挖掘结构中删除列 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd8691d8ec0cc1546e27e8195e7d0bbc20709f59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209685"
---
# <a name="remove-columns-from-a-mining-structure"></a>从挖掘结构中删除列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在已创建挖掘结构后，可以使用数据挖掘设计器删除挖掘结构中的列。 删除挖掘结构列的原因可能包括以下几种：  
  
-   挖掘结构包含某个列的多个副本并且您想要在模型中避免使用重复数据。  
  
-   数据应受到保护，但启用了钻取功能。  
  
-   数据未在建模中使用并且不应处理。  
  
 从挖掘结构中删除某一列并不会在数据源视图或外部数据中更改该列；只有元数据被删除。 但在您更改在挖掘结构中使用的列时，必须重新处理挖掘结构以及基于该结构的所有模型。  
  
### <a name="to-remove-a-column-from-the-mining-structure"></a>从挖掘结构中删除列  
  
1.  在数据挖掘设计器中选择 **“挖掘结构”** 选项卡。  
  
2.  展开挖掘结构树，以显示所有列。  
  
3.  右键单击要删除的列，再选择“删除”  。  
  
4.  在 **“删除对象”** 对话框中，单击 **“确定”** 。  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
