---
title: 添加或删除表或视图中数据源视图 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.tablespane.f1
helpviewer_keywords:
- deleting tables
- tables [Analysis Services]
- removing tables
- adding tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 98307d04-6548-4d7d-9244-2371dd165249
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc78ad1f8a1f49d1a42c5b2ded45a913cdd7e669
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117947"
---
# <a name="adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services"></a>在数据源视图中添加或删除表或视图 (Analysis Services)
  在您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建了数据源视图 (DSV) 后，可以通过添加或删除表和列，包括来自其他数据源的表和列，在数据源视图设计器中修改数据源视图。  
  
 若要在数据源视图设计器中打开该 DSV，请在解决方案资源管理器中双击该 DSV。 一旦打开该 DSV 后，可使用按钮栏或菜单上的“添加/删除表”命令来修改或扩展该 DSV。 您还可以在关系图中使用这些对象。 例如，您可以选择某一对象，然后使用键盘上的 Delete 键删除对象。  
  
> [!WARNING]  
>  删除表时要格外小心。 删除表将从 DSV 中删除所有关联列和关系，并且将使绑定到该表的所有对象失效。  
  
## <a name="selecting-tables-or-views-to-add-or-remove"></a>选择要添加或删除的表或视图  
 使用“添加/删除表”对话框，可以在“可用对象”和“包含的对象”列表之间移动表或视图。 **“可用对象”** 列表最初包含主数据源中还没有位于数据源视图中的所有表或视图。 如果主数据源支持`OPENROWSET`函数，您还可以添加表或视图从其他数据源中的项目或数据库。  
  
 在将表添加到 DSV 中或者从 DSV 中删除表时，还会将该表添加到 DSV 的当前选定关系图中或从中删除。 关系图的详细信息，请参阅[使用的数据源视图设计器中的关系图&#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md)。  
  
 在“添加/删除表”对话框中将表移至“包含的对象”列表后，可以添加所有相关表。 如果数据源中存在外键约束，此操作将根据该外键约束添加表。 如果不存在外键约束，则可以使用`NameMatchingCriteria`要通过指定要生成可能关系的表中的列名称匹配的条件来确定关系的数据源视图的属性。 如果`NameMatchingCriteria`属性指定的数据源视图中，单击**添加相关表**即可从具有匹配列名的数据源添加表。 有关设置的详细信息`NameMatchingCriteria`属性，请参阅[多维模型中的数据源视图](data-source-views-in-multidimensional-models.md)。  
  
> [!NOTE]  
>  向数据源视图中添加对象或从中删除对象不会影响基础数据源。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的数据源视图](data-source-views-in-multidimensional-models.md)   
 [使用的数据源视图设计器中的关系图&#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
