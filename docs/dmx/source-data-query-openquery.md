---
title: OPENQUERY (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f7b4744c3f521ed4c51e461f2b01a748b9b6496
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842470"
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
  
## <a name="remarks"></a>Remarks  
 **OPENQUERY**提供了一种更安全的方法，以支持数据源权限访问外部数据。 由于连接字符串存储在数据源中，因此管理员可以使用数据源的属性来管理对数据的访问。 有关数据源的详细信息，请参阅[支持数据源&#40;SSAS-多维&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)。  
  
 你可以通过查询是服务器上可用的数据源列表**MDSCHEMA_INPUT_DATASOURCES**架构行集。 有关使用**MDSCHEMA_INPUT_DATASOURCES**，请参阅[MDSCHEMA_INPUT_DATASOURCES 行集](../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)。  
  
 还可以通过使用下面的 DMX 查询来返回当前 Analysis Services 数据库中的数据源的列表：  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>示例  
 下面的示例使用 MyDS 数据源中已定义[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库以创建连接到[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据库和查询**vTargetMail**视图。  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>请参阅  
 [&#60;源数据查询&#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
