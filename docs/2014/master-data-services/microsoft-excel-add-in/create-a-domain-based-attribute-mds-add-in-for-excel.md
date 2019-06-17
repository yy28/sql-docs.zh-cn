---
title: 创建基于域的属性 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 296ace8d97269d80179d437b1033b92196d6adc5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478987"
---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>创建基于域的属性（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，管理员在想要将列中的值限制为一组特定值时可以创建基于域的属性。  
  
 这些值可以已处于工作表中，也可以来自某一现有实体。  
  
> [!NOTE]  
>  如果用户在该约束列键入某个值，而不是从列表中进行选择，则在用户发布时将在 **$InputStatus$** 列中显示错误。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域和 **“资源管理器”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../administrators-master-data-services.md)。  
  
-   模型和实体必须已经存在。  
  
### <a name="to-perform-this-procedure"></a>若要执行此过程：  
  
1.  在 Excel 中，加载包含要约束的列（属性）的实体。 有关详细信息，请参阅[将数据加载到 Excel 的 mds](export-data-to-excel-from-master-data-services.md)。  
  
2.  单击要约束的列中的任意单元。  
  
3.  在 **“生成模型”** 组中，单击 **“特性属性”** 。  
  
4.  在“特性属性”  对话框的“属性类型”  列表中，选择“约束列表(基于域)”  。  
  
5.  在 **“使用以下位置的值填充属性”** 列表中：  
  
    -   若要使用工作表中的值，请选择 **“所选列”** 。 将使用所选列中的值创建新实体和新的临时表。  
  
    -   若要使用现有实体中的值，请选择该实体的名称。  
  
6.  如果您在前一步骤中选择 **“所选列”** ，则在 **“新实体名称”** 框中键入新实体的名称。 该名称可与列（属性）名称相同。  
  
7.  单击“确定”  。 列中的每个单元现在都有一个可供用户从中选择的值列表。  
  
## <a name="next-steps"></a>后续步骤  
  
-   若要在约束列表中添加和删除值，请加载属性基于的实体。 有关加载实体的详细信息，请参阅[将数据加载到 Excel 的 mds](export-data-to-excel-from-master-data-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [基于域的属性 (Master Data Services)](../domain-based-attributes-master-data-services.md)   
 [创建实体（用于 Excel 的 MDS 外接程序）](create-an-entity-mds-add-in-for-excel.md)   
 [生成模型（用于 Excel 的 MDS 外接程序）](building-a-model-mds-add-in-for-excel.md)  
  
  
