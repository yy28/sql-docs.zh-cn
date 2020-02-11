---
title: OPENROWSET （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8be3fe8cbf30121ec2895f59306c925a422d5c39
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938127"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;源数据查询&gt; -OPENROWSET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用对外部访问接口的查询替换源数据查询。 INSERT，选择 "从预测联接"，然后从 "自然预测联接语句" 中选择 "支持**OPENROWSET**"。  
  
## <a name="syntax"></a>语法  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>参数  
 *provider_name*  
 OLE DB 访问接口名称。  
  
 *provider_string*  
 用于指定的访问接口的 OLE DB 连接字符串。   
  
 *query_syntax*  
 一个返回行集的查询语法。  
  
## <a name="remarks"></a>备注  
 数据挖掘提供程序将使用*provider_name*和 provider_string 建立与数据源对象的连接，并将执行*query_syntax*中指定的查询 *，* 以便从源数据中检索行集。  
  
## <a name="examples"></a>示例  
 以下示例可用于 PREDICTION JOIN 语句中，通过使用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] SELECT 语句检索 [!INCLUDE[tsql](../includes/tsql-md.md)] 数据库中的数据。  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#60;源数据查询&#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 &#40;DMX&#41; 语句参考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
