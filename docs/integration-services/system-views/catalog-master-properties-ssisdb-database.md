---
title: catalog.master_properties（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8de63d58afdb891039c1037e24b58f78c73dd581
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052779"
---
# <a name="catalogmaster_properties-ssisdb-database"></a>catalog.master_properties（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master 的属性。

|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|scale out master 属性的名称。|  
|property_value|**nvarchar(max)**|scale out master 属性的值。|

## <a name="remarks"></a>备注
此视图每行显示一个 scale out master 属性。 此视图显示的属性包括如下：

|属性名称|说明|  
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
