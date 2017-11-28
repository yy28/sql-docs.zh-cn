---
title: "OPENQUERY (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: OPENQUERY
dev_langs: DMX
helpviewer_keywords: OPENQUERY statement
ms.assetid: fe57f3a3-a8e6-402c-995e-bd2fe28a7a7c
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2348e0caf4eee97a6fae2e566ca534e65c70ae72
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;源数据查询&gt;-OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  将源数据查询替换为对现有数据源的查询。 插入、 选择从 PREDICTION JOIN，和选择从 NATURAL PREDICTION JOIN 语句支持**OPENQUERY**。  
  
## <a name="syntax"></a>语法  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>参数  
 *命名的数据源*  
 数据源上是否存在[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库。  
  
 *查询语法*  
 一个返回行集的查询语法。  
  
## <a name="remarks"></a>注释  
 **OPENQUERY**提供了一种更安全的方法，以支持数据源权限访问外部数据。 由于连接字符串存储在数据源中，因此管理员可以使用数据源的属性来管理对数据的访问。 有关数据源的详细信息，请参阅[支持数据源 &#40;SSAS-多维 &#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
 你可以通过查询是服务器上可用的数据源列表**MDSCHEMA_INPUT_DATASOURCES**架构行集。 有关使用**MDSCHEMA_INPUT_DATASOURCES**，请参阅[MDSCHEMA_INPUT_DATASOURCES 行集](../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)。  
  
 还可以通过使用下面的 DMX 查询来返回当前 Analysis Services 数据库中的数据源的列表：  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>示例  
 下面的示例使用 MyDS 数据源中已定义[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库以创建连接到[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据库和查询**vTargetMail**视图。  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#60; 源数据查询 &#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
