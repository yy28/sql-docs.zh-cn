---
title: "catalog.create_environment_variable （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 91ed017b-6567-4bf2-b9f1-e2b5c70a5343
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 5636651cccbb43c6c1627d1f28eccd9b3f9b5b0d
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateenvironmentvariable-ssisdb-database"></a>catalog.create_environment_variable（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中创建环境变量。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.create_environment_variable [@folder_name =] folder_name  
    , [@environment_name =] environment_name  
    , [@variable_name =] variable_name  
    , [@data_type =] data_type  
    , [@sensitive =] sensitive  
    , [@value =] value  
    , [@description =] description  
```  
  
## <a name="arguments"></a>参数  
 [@folder_name =] *folder_name*  
 包含环境的文件夹的名称。 *Folder_name*是**nvarchar （128)**。  
  
 [@environment_name =] *environment_name*  
 环境的名称。 *Environment_name*是**nvarchar （128)**。  
  
 [@variable_name =] *variable_name*  
 环境变量的名称。 *Variable_name*是**nvarchar （128)**。  
  
 [@data_type =] *data_type*  
 变量的数据类型。 支持环境变量数据类型包括**布尔**，**字节**， **DateTime**， **Double**， **Int16**， **Int32**， **Int64**，**单个**，**字符串**， **UInt32**，和**UInt64**。 不支持的环境变量数据类型包括**Char**， **DBNull**，**对象**，和**Sbyte**。 数据类型*data_type*参数是**nvarchar （128)**。  
  
 [@sensitive =]*敏感*  
 指示变量是否包含敏感值。 使用值 `1` 表示环境变量的值是敏感值，值为 `0` 表示该值不是敏感值。 存储敏感值时将对其加密。 一个值，不是敏感数据是以纯文本形式存储。*敏感*是**位**。  
  
 [@value =]*值*  
 环境变量的值。 *值*是**sql_variant**。  
  
 [@description =]*说明*  
 环境变量的说明。 *值*是**nvarchar(1024)**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对环境的 READ 和 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   文件夹名称、环境名称或环境变量名无效  
  
-   环境中已存在此变量名  
  
-   用户没有适当的权限  
  
## <a name="remarks"></a>注释  
 可以使用环境变量高效地将值分配给项目参数或包参数，以用于执行包。 环境变量启用参数值的排列。 变量名在环境中必须是唯一的。  
  
 此存储过程验证变量的数据类型，以确保它受 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录支持。  
  
> [!TIP]  
>  请考虑使用**Int16**中数据类型[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]而不是使用不受支持**Sbyte**数据类型。  
  
 值传递给使用此存储过程*值*参数转换从[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]数据类型设置为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]根据下表的数据类型：  
  
|Integration Services 数据类型|SQL Server 数据类型|  
|------------------------------------|--------------------------|  
|**Boolean**|**bit**|  
|**字节**|**二进制**， **varbinary**|  
|**DateTime**|**datetime**， **datetime2**， **datetimeoffset**， **smalldatetime**|  
|**双精度**|精确数字：**十进制**，**数值**;近似数值： **float**，**实际**|  
|**Int16**|**int**|  
|**Int32**|**int**|  
|**Int64**|**bigint**|  
|**Single**|精确数字：**十进制**，**数值**;近似数值： **float**，**实际**|  
|**字符串**|**varchar**， **nvarchar**， **char**|  
|**UInt32**|**int** (**int**最接近的可用映射到**Uint32**。)|  
|**UInt64**|**bigint** (**int**最接近的可用映射到**Uint64**。)|  
  
  

