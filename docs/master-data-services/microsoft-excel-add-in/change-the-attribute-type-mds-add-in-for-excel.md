---
title: "更改属性类型 (MDS Add-in for Excel) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: aafb37debc437fa6f2aee678eba571d8bd23ec5e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="change-the-attribute-type-mds-add-in-for-excel"></a>更改属性类型（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，数据类型或允许的字符数不正确时，管理员可以更改属性类型。  
  
 如果要更改属性类型以创建受限制列表（基于域的属性），请参阅[创建基于域的属性（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)。  
  
> [!NOTE]  
>  不能更新“名称”或“代码”列的类型或长度。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域和 **“资源管理器”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../../master-data-services/administrators-master-data-services.md)。  
  
-   必须存在现有的模型、实体和属性。  
  
### <a name="to-change-the-attribute-type"></a>更改属性类型  
  
1.  在 Excel 中，加载包含要更改的列（属性）的实体。 有关详细信息，请参阅 [从 Master Data Services 中将数据导出至 Excel](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)。  
  
2.  单击要更改的列中的任意单元。  
  
3.  在 **“生成模型”** 组中，单击 **“特性属性”**。  
  
4.  在 **“特性属性”** 对话框中，根据需要更新设置。  
  
5.  单击 **“确定”**。  
  
## <a name="what-happens-when-you-change-the-attribute-type"></a>在更改属性类型时会发生什么情况？  
 如果属性没有任何依赖项，例如属性被 MDS 业务规则或派生层次结构引用，则无法更改属性的数据类型。 获取一个错误，指出无法修改属性类型，因为它被对象引用。  
  
 如果属性值的数据类型在转换期间出错，则 MDS 将执行以下操作。  
  
-   更改属性的数据类型。  
  
-   生成包含之前值的带有后缀“_old”的属性的副本。 这称为弃用的属性。  
  
## <a name="see-also"></a>另请参阅  
 [属性 (Master Data Services)](../../master-data-services/attributes-master-data-services.md)   
 [生成模型（用于 Excel 的 MDS 外接程序）](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  
