---
title: "catalog.configure_catalog（SSISDB 数据库）| Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7edd093ee4804c8c0c01a5638fd7df519f4564bc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  通过将目录属性设置为指定的值，配置 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录。  
  
## <a name="syntax"></a>语法  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>参数  
 [ @property_name =] *property_name*  
 目录属性的名称。 Property_name 为 nvarchar(255) 。 有关可用属性的详细信息，请参阅 [catalog.catalog_properties（SSISDB 数据库）](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)。  
  
 [ @property_value = ] *property_value*  
 目录属性的值。 Property_value 为 nvarchar(255) 。 有关属性值的详细信息，请参阅 [catalog.catalog_properties（SSISDB 数据库）](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 此存储过程确定 property_value 对于每个 property_name 是否有效。  
  
 仅当没有活动的执行（如挂起、排队、正在运行、暂停的执行）时，才能执行此存储过程。  
  
 正在配置目录时，所有其他目录存储过程都将失败，并显示错误消息“当前正在配置服务器”。
  
 当配置目录时，将向操作记录中写入一个条目。  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   ssis_admin 数据库角色的成员资格  
  
-   sysadmin 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   属性不存在  
  
-   属性值无效  
  
  
