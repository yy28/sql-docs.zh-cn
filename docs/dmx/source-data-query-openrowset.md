---
title: OPENROWSET (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 43431be3f68bc7146d9e5a6cc137100ec384c960
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842110"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;源数据查询&gt;-OPENROWSET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用对外部访问接口的查询替换源数据查询。 插入、 选择从 PREDICTION JOIN，和选择从 NATURAL PREDICTION JOIN 语句支持**OPENROWSET**。  
  
## <a name="syntax"></a>语法  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>参数  
 provider_name  
 OLE DB 访问接口名称。  
  
 *provider_string*  
 用于指定的访问接口的 OLE DB 连接字符串。   
  
 *query_syntax*  
 一个返回行集的查询语法。  
  
## <a name="remarks"></a>Remarks  
 数据挖掘提供程序将通过使用建立到数据源对象的连接*provider_name*和*provider_string* ，会执行中指定的查询*query_syntax*源数据中检索行集。  
  
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
  
## <a name="see-also"></a>请参阅  
 [&#60;源数据查询&#62;](../dmx/source-data-query.md)   
 [数据挖掘扩展插件&#40;DMX&#41;数据操作语句](../dmx/dmx-statements-data-manipulation.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
