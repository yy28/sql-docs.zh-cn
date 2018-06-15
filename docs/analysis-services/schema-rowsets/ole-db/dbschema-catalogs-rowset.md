---
title: DBSCHEMA_CATALOGS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61e4de1591752919a5916d6044591bda49b14992
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34033308"
---
# <a name="dbschemacatalogs-rowset"></a>DBSCHEMA_CATALOGS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识可从数据库管理系统 (DBMS) 中访问的目录的关联物理属性。  
  
## <a name="rowset-columns"></a>行集列  
 **DBSCHEMA_CATALOGS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|255|目录名称。 不可为 null。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||可读的表说明。|  
|**角色**|**DBTYPE_WSTR**||当前用户所属角色的逗号分隔列表。<br /><br /> 星号 (\*) 是包括作为角色，如果当前用户是服务器或数据库管理员。<br /><br /> **用户名**追加到**角色**如果角色之一使用动态安全。|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||相应目录上次修改的日期。|  
  
 行集按排序**CATALOG_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **DBSCHEMA_CATALOGS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB 架构行集合](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
