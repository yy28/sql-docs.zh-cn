---
description: LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER
title: LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 626b73d3-a257-4b45-82fb-c6299faa0001
author: stevestein
ms.author: sstein
ms.openlocfilehash: d29d8e02729b78814ac7bdb045535953c4b5ced7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88329343"
---
# <a name="localdb_error_cannot_create_instance_folder"></a>LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>详细信息  
  
| Attribute | 值 |
| --------- | ----- |
|产品名称|SQL Server|  
|事件 ID|256|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|无法在以下位置创建本地数据库实例的文件夹：%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server 本地 DB\Instances \\<实例名称 \> 。|  
  
## <a name="explanation"></a>说明  
 不能在 %userprofile% 下创建文件夹。  
  
## <a name="user-action"></a>用户操作  
  
