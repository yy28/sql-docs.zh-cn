---
title: OPENQUERY （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: caac43eb176e17a6e92e487f3dedae71a252f5af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68887730"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;源数据查询&gt; -OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  将源数据查询替换为对现有数据源的查询。 INSERT，从预测联接中选择，并从自然预测联接语句中选择 "支持**OPENQUERY**"。  
  
## <a name="syntax"></a>语法  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>参数  
 *命名数据源*  
 数据库中存在[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的数据源。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
 *查询语法*  
 一个返回行集的查询语法。  
  
## <a name="remarks"></a>备注  
 **OPENQUERY**通过支持数据源权限提供了一种更安全的访问外部数据的方法。 由于连接字符串存储在数据源中，因此管理员可以使用数据源的属性来管理对数据的访问。 有关数据源的详细信息，请参阅[支持的数据源 &#40;SSAS-多维&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional)。  
  
 可以通过查询**MDSCHEMA_INPUT_DATASOURCES**架构行集来获取服务器上可用的数据源的列表。 有关使用**MDSCHEMA_INPUT_DATASOURCES**的详细信息，请参阅[MDSCHEMA_INPUT_DATASOURCES 行集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset)。  
  
 还可以通过使用下面的 DMX 查询来返回当前 Analysis Services 数据库中的数据源的列表：  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>示例  
 下面的示例使用[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库中已定义的 MyDS 数据源来创建与[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据库的连接，并查询**vTargetMail**视图。  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#60;源数据查询&#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
