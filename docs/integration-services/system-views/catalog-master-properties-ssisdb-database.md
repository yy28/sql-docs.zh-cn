---
title: catalog.master_properties（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 57941951cbf442b275b349a753ae8aa73c69668f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master 的属性。

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|scale out master 属性的名称。|  
|property_value|**nvarchar(max)**|scale out master 属性的值。|

## <a name="remarks"></a>Remarks
此视图每行显示一个 scale out master 属性。 此视图显示的属性包括如下：

|属性名称|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|日志数据库所在的 SQL Server。|
|**LAST_ONLINE_TIME**|Scale Out Master 上次在线的时间。|
|**MACHINE_IP**|计算机的 IP。|
|**MACHINE_NAME**|计算机的名称。|
|**MASTER_ADDRESS**|Scale Out Master 的终结点。|
|**MASTER_SERVICE_PORT**|Scale Out Master 终结点中的端口。|
|**SSLCERT_THUMBPRINT**|Scale Out Master 证书的指纹。|

## <a name="permissions"></a>权限
具有公共数据库角色的所有成员均有权读取此视图。 
