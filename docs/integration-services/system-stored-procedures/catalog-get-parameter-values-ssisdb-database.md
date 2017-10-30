---
title: "catalog.get_parameter_values （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5b1aeaf7-c938-4aef-bafc-e4d7a82eb578
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4ad8f0c367e38581db696d2aa32afd5b92d635d2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="cataloggetparametervalues-ssisdb-database"></a>catalog.get_parameter_values（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中的项目和对应包中解析和检索默认参数值。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.get_parameter_values [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id  ]  
  
```  
  
## <a name="arguments"></a>参数  
 [ @folder_name =] *folder_name*  
 包含项目的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [ @project_name =]*文件的内容*  
 参数所在的项目的名称。 *文件的内容*是**nvarchar （128)**。  
  
 [ @package_name =]*包名称*  
 包的名称。 指定包名称，以便从特定包中检索所有项目参数和参数。 使用 NULL 可以从所有包中检索所有项目参数和参数。 *Package_name*是**nvarchar(260)**。  
  
 [ @reference_id =] *reference_id*  
 环境引用的唯一标识符。 此参数可选。 *Reference_id*是**bigint**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 返回具有以下格式的表：  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_type|**int**|参数的类型。 对于项目参数，该值是 `20`；对于包参数，值是 `30`。|  
|parameter_data_type|**nvarchar （128)**|参数的数据类型。|  
|parameter_name|**sysname**|参数名。|  
|parameter_value|**sql_variant**|参数的值。|  
|sensitive|**bit**|当值为 `1` 时，参数值是敏感的。 当值为 `0` 时，参数值是不敏感的。|  
|required|**bit**|如果值为 `1`，则需要参数值才能开始执行。 如果值为 `0`，则不需要参数值即可开始执行。|  
|value_set|**bit**|如果值为 `1`，则已分配参数值。 如果值为 `0`，则尚未分配参数值。|  
  
> [!NOTE]  
>  以纯文本形式显示文本值。 **NULL**显示代替敏感值。  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对项目的 READ 权限，如果适用，则包含针对引用环境的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   在指定的文件夹或项目中找不到该包  
  
-   用户没有适当的权限  
  
-   指定的环境引用不存在  
  
  

