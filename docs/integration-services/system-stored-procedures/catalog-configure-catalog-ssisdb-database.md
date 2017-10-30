---
title: "catalog.configure_catalog （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 15bec231bf1de825cea952e07827074d56751386
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  通过将目录属性设置为指定的值，配置 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录。  
  
## <a name="syntax"></a>语法  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>参数  
 [ @property_name =] *property_name*  
 目录属性的名称。 *Property_name*是**nvarchar （255)**。 有关可用属性的详细信息，请参阅[catalog.catalog_properties &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
 [ @property_value =] *property_value*  
 目录属性的值。 *Property_value*是**nvarchar （255)**。 有关属性值的详细信息，请参阅[catalog.catalog_properties &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 此存储的过程确定是否*property_value*对每个有效*property_name*。  
  
 仅当没有活动的执行（如挂起、排队、正在运行、暂停的执行）时，才能执行此存储过程。  
  
 正在配置的目录，而所有其他目录存储过程失败并显示错误消息"当前正在配置服务器。"
  
 当配置目录时，将向操作记录中写入一个条目。  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   属性不存在  
  
-   属性值无效  
  
  

