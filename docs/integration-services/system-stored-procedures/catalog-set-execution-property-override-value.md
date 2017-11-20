---
title: "catalog.set_execution_property_override_value |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 20f2c882a78f5e60931b0152d5877898e1972d0a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetexecutionpropertyoverridevalue"></a>catalog.set_execution_property_override_value
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的执行实例设置属性的值。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>参数  
 [ @execution_id =] *execution_id*  
 执行实例的唯一标识符。 *Execution_id*是**bigint**。  
  
 [ @property_path =] *property_path*  
 指向包中属性的路径。 *Property_path*是**nvarchar （4000)**。  
  
 [ @property_value =] *property_value*  
 要赋给该属性的覆盖值。 *Property_value*是**nvarchar (max)**。  
  
 [ @sensitive =]*敏感*  
 当值为 1 时，属性是敏感的并在存储时加密。 当值为 0 时，属性是不敏感的并以纯文本形式存储值。 *敏感*自变量是**位**。  
  
## <a name="remarks"></a>注释  
 此过程执行相同的功能**属性重写**主题中**高级**选项卡**执行包**对话框。 属性的路径派生自**包路径**包任务的属性。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   用户没有适当的权限  
  
-   执行标识符无效  
  
-   属性路径无效  
  
-   属性值的数据类型与属性的数据类型不匹配  
  
## <a name="see-also"></a>另请参阅  
 [catalog.set_execution_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  

