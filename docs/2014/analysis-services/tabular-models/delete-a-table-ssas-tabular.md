---
title: 删除表（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
author: minewiskan
ms.author: owend
ms.openlocfilehash: c72fa90426440c1be84318a15cf0d761ef16aca8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939700"
---
# <a name="delete-a-table-ssas-tabular"></a>删除表（SSAS 表格）
  在模型设计器中，您可以删除不再需要的模型工作区数据库中的表。 删除表并不影响原始源数据，只会影响你已导入并且正在使用的数据。 您无法撤消对表的删除。  
  
### <a name="to-delete-a-table"></a>删除表  
  
-   对于想要删除的表，右键单击模型设计器底部的选项卡，然后单击“删除”****。  
  
## <a name="considerations-when-deleting-tables"></a>删除表时的注意事项  
  
-   在您删除一个表时，该表位于其上的整个选项卡都将被删除。  
  
-   如果任何度量值与该表相关联，则也将删除该度量值的定义。  
  
-   如果您使用该表创建了任何计算列，则也删除该表中的列；其他表中使用已删除表中的列的任何计算列将显示一个错误。  
  
## <a name="see-also"></a>另请参阅  
 [表和列（SSAS 表格）](tables-and-columns-ssas-tabular.md)  
  
  
