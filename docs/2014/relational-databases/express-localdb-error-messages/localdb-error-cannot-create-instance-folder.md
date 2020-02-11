---
title: LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 626b73d3-a257-4b45-82fb-c6299faa0001
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a5375c391b976de111813f55d422a367b3ea874a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62519541"
---
# <a name="localdb_error_cannot_create_instance_folder"></a>LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|256|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|无法在以下位置创建本地数据库实例的文件夹：%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server 本地\\ DB\Instances<实例\>名称。|  
  
## <a name="explanation"></a>说明  
 不能在 %userprofile% 下创建文件夹。  
  
## <a name="user-action"></a>用户操作  
  
