---
title: "catalog.remove_data_tap |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2f2c9b5d9333c201120e5f3a3e392c59012a8ac7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从执行中的组件输出删除数据分流点。 数据分流点的唯一标识符与执行实例相关联。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>参数  
 [ @data_tap_id =] *data_tap_id*  
 使用 catalog.add_data_tap 存储过程创建的数据分流点的唯一标识符。 *Data_tap_id*是**bigint**。  
  
## <a name="remarks"></a>注释  
 如果包中包含名称相同的多个数据流任务，则将数据分流点添加到具有给定名称的第一个数据流任务。  
  
## <a name="return-codes"></a>返回代码  
 0（成功）  
  
 存储过程失败时引发错误。  
  
## <a name="result-set"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 若要删除数据点击，执行的实例必须位于创建状态 (值为 1 中**状态**列[catalog.operations &#40;SSISDB 数据库 &#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)视图)。  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对执行实例的 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下表说明了导致存储过程失败的情况。  
  
-   用户没有 MODIFY 权限。  
  
## <a name="see-also"></a>另请参阅  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  

