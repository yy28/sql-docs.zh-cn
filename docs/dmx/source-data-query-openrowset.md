---
title: OPENROWSET (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8be3fe8cbf30121ec2895f59306c925a422d5c39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938127"
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;源数据查询&gt;的 OPENROWSET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用对外部访问接口的查询替换源数据查询。 INSERT、 SELECT FROM PREDICTION JOIN，和 SELECT FROM NATURAL PREDICTION JOIN 语句支持**OPENROWSET**。  
  
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
  
## <a name="remarks"></a>备注  
 数据挖掘提供程序将通过使用建立与数据源对象的连接*provider_name*并*provider_string*并将执行中指定的查询*query_syntax*来检索源数据中的行集。  
  
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
  
  
