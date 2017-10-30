---
title: "catalog.master_properties （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 0fcbdca57c7764eaec758d2ad9ef3ab8675a3a9b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties （SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

显示的属性[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]缩放出 Master。

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|主属性扩展的名称。|  
|property_value|**nvarchar(max)**|主属性扩展的值。|

## <a name="remarks"></a>注释
此视图显示每个扩展主属性行。 此视图显示的属性包括如下：

|属性名称|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|在中找到日志数据库的 SQL Server。|
|**LAST_ONLINE_TIME**|当缩放出 Master 为联机的最后时间。|
|**MACHINE_IP**|计算机的 IP。|
|**MACHINE_NAME**|计算机的名称。|
|**MASTER_ADDRESS**|缩放出主终结点。|
|**MASTER_SERVICE_PORT**|中的缩放出主终结点的端口。|
|**SSLCERT_THUMBPRINT**|缩放出主证书的指纹。|

## <a name="permissions"></a>Permissions
公共数据库角色的所有成员具有都读取此视图的权限。 

