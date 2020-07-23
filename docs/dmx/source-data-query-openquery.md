---
title: OPENQUERY （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a075f314af0eb8ea2eb0bc941ada0bc38e22fec3
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970397"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;源数据查询 &gt; -OPENQUERY
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  将源数据查询替换为对现有数据源的查询。 INSERT，从预测联接中选择，并从自然预测联接语句中选择 "支持**OPENQUERY**"。  
  
## <a name="syntax"></a>语法  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>参数  
 *命名数据源*  
 数据库中存在的数据源 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。  
  
 *查询语法*  
 一个返回行集的查询语法。  
  
## <a name="remarks"></a>备注  
 **OPENQUERY**通过支持数据源权限提供了一种更安全的访问外部数据的方法。 由于连接字符串存储在数据源中，因此管理员可以使用数据源的属性来管理对数据的访问。 有关数据源的详细信息，请参阅[支持的数据源 &#40;SSAS-多维&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional)。  
  
 可以通过查询**MDSCHEMA_INPUT_DATASOURCES**架构行集来获取服务器上可用的数据源的列表。 有关使用**MDSCHEMA_INPUT_DATASOURCES**的详细信息，请参阅[MDSCHEMA_INPUT_DATASOURCES 行集](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126243(v=sql.110))。  
  
 还可以通过使用下面的 DMX 查询来返回当前 Analysis Services 数据库中的数据源的列表：  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>示例  
 下面的示例使用数据库中已定义的 MyDS 数据源 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 来创建与数据库的连接 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] ，并查询**vTargetMail**视图。  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#60;源数据查询&#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
