---
title: 名称匹配 （数据源视图向导） (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.namematchingcriteria.f1
ms.assetid: 7f811e02-0fe6-45c9-a7b7-29c61032d96b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 866bdea710033a0cfa3bdadb34282c96c810d730
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072398"
---
# <a name="name-matching-data-source-view-wizard-analysis-services"></a>名称匹配（数据源视图向导）(Analysis Services)
  可以使用 **“名称匹配”** 页，针对为数据源视图选择的表以及架构中的其他表，选择用于检测它们之间可能存在的关系的条件。 如果这些表之间不存在物理外键关系，则可以使用所选的条件帮助标识相关的表并将这些表添加到数据源视图中。 通过名称匹配标识的逻辑关系也可以添加到数据源视图中。  
  
> [!NOTE]  
>  只有在您选择的数据源包含多个表，并且这些表中的任意表之间都没有外键关系时，此页才会显示。  
  
## <a name="options"></a>选项  
 **通过匹配列创建逻辑关系**  
 选择此项可使用名称匹配条件，针对您选择的要包含在数据源视图中的表以及架构中的其他表，检测它们之间可能的逻辑依赖关系和关系。 如果清除此复选框，则不会使用任何名称匹配条件来标识数据源中表之间的逻辑关系。  
  
 **外键匹配**  
 选择用于在数据源中的表与视图之间创建逻辑关系的条件。 匹配字符串中将忽略非字母数字字符。 例如，“Customer ID”、“Customer_ID”和“CustomerID”相互匹配。 选择下表中的选项之一可在指定条件下创建关系：  
  
|选择|执行的创建操作|  
|------------|---------------|  
|**与主键同名**|对于任何表，只要其中包含的任意一列的名称与所选表的主键列名相匹配，就创建与该表之间的逻辑关系。|  
|**与目标表同名**|对于任何表，只要其中包含的任意一列的名称与所选表的名称相匹配，就创建与该表之间的逻辑关系。|  
|**目标表名 + 主键名**|对于任何表，只要其中包含的任意一列的名称与所选表的名称和主键列名按该顺序连在一起的所选表的名称相匹配，就创建与该表之间的逻辑关系。 该连接形式中的非字母数字字符将被忽略（例如，“Product ID”、“Product_ID”和“ProductID”相互匹配）。|  
  
 **说明和示例**  
 查看所选条件的说明和示例。  
  
  
