---
title: 查询用于创建挖掘模型的参数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- content queries [DMX]
ms.assetid: ce7719e0-6127-4d9c-a753-0e0a3db065e1
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee19f34f99c51bd1747718e5d34fd6ab12fe3e49
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288343"
---
# <a name="query-the-parameters-used-to-create-a-mining-model"></a>查询用于创建挖掘模型的参数
  挖掘模型的构成不仅受到定型事例的影响，还会受到在创建模型时设置的参数的影响。 因此，检索现有模型的参数设置以便更好地理解模型的行为可能会很有用。 在归档该模型的特定版本时检索参数可能也很有用。  
  
 若要查找在创建模型时使用的参数，应针对某个挖掘模型架构行集创建查询。 在 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]中，这些架构行集将作为可使用 Transact-SQL 语法轻松查询的一组系统视图公开。 下面的过程介绍如何创建返回用于创建指定挖掘模型的参数的查询。  
  
### <a name="to-open-a-query-window-for-a-schema-rowset-query"></a>打开架构行集查询的“查询”窗口  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开包含要查询的模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
2.  右键单击实例名称，选择“新建查询”，然后选择“DMX”。  
  
    > [!NOTE]  
    >  还可以通过使用 **MDX** 模板来针对数据挖掘模型创建查询。  
  
3.  如果实例包含多个数据库，应从工具栏中的 **“可用数据库”** 列表中选择包含要查询的模型的数据库。  
  
### <a name="to-return-model-parameters-for-an-existing-mining-model"></a>从现有挖掘模型中返回模型参数  
  
1.  在 DMX 查询窗格中，键入或粘贴以下文本：  
  
    ```  
    SELECT MINING_PARAMETERS  
    FROM $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = ''  
    ```  
  
2.  在对象资源管理器中，选择需要的挖掘模型，然后将它拖到 DMX 查询窗格中的单引号之间。  
  
3.  按 F5，或单击 **“执行”**。  
  
## <a name="example"></a>示例  
 下面的代码返回用于创建在 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md)中生成的挖掘模型的参数列表。 这些参数包括服务器上的提供程序中可用的挖掘服务所使用的任何默认参数的显式值。  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
 代码示例返回聚类分析模型的下列参数：  
  
 示例结果：  
  
 MINING_PARAMETERS  
  
 CLUSTER_COUNT=10,CLUSTER_SEED=0,CLUSTERING_METHOD=1,MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_STATES=100,MINIMUM_SUPPORT=1,MODELLING_CARDINALITY=10,SAMPLE_SIZE=50000,STOPPING_TOLERANCE=10  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘查询任务和操作指南](data-mining-query-tasks-and-how-tos.md)   
 [数据挖掘查询](data-mining-queries.md)  
  
  
