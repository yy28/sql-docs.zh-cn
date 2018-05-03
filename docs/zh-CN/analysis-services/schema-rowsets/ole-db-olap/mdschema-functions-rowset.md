---
title: MDSCHEMA_FUNCTIONS 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDSCHEMA_FUNCTIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_FUNCTIONS rowset
ms.assetid: 5253fa8c-b1ce-4504-aff6-a246b5e675c7
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c26528fd259dbb950d29b36271cd60be6bb05b5a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mdschemafunctions-rowset"></a>MDSCHEMA_FUNCTIONS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  介绍可用于已连接到数据库的客户端应用程序的函数。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_FUNCTIONS**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|函数的名称。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|函数的说明。|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**|以逗号分隔的参数列表，采用与 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 中类似的格式。 例如，某参数可以为 Name as String。|  
|**RETURN_TYPE**|**DBTYPE_I4**|**VARTYPE**的函数的返回数据类型。|  
|**源**|**DBTYPE_I4**|函数的来源：<br /><br /> 1 表示 MDX 函数。<br /><br /> 2 表示用户定义函数。|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|用户定义函数的接口名称<br /><br /> 多维表达式 (MDX) 函数的组名。|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|用户定义函数的类型库名称。 **NULL** MDX 函数。|  
|**DLL_NAME**|**DBTYPE_WSTR**|（可选）实现用户定义函数的程序集的名称。<br /><br /> 返回**VT_NULL** MDX 函数。|  
|**HELP_FILE**|**DBTYPE_WSTR**|（可选）包含用户定义函数帮助文档的文件名。<br /><br /> 返回**VT_NULL** MDX 函数。|  
|**HELP_CONTEXT**|**DBTYPE_I4**|（可选）返回此函数的帮助上下文 ID。|  
|**OBJECT**|**DBTYPE_WSTR**|（可选）应用了属性的对象类的通用名称。 例如，行集对应 < level_name >。成员函数将返回"**级别**"。<br /><br /> 返回**VT_NULL**对于用户定义函数或非属性 MDX 函数。|  
|**标题**|**DBTYPE_WSTR**|函数的显示标题。|  
  
 行集按排序**原点**， **INTERFACE_NAME**， **FUNCTION_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_FUNCTIONS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**FUNCTION_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**源**|**DBTYPE_I4**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
