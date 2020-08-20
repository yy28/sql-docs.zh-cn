---
description: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
title: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: fa082dca-bf88-46e7-b61e-7ac8835a3493
author: stevestein
ms.author: sstein
ms.openlocfilehash: bc5e696b75b1f1a011c380d77010ca3167187a3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470517"
---
# <a name="localdb_error_unknown_language_id"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>详细信息  
  
| Attribute | 值 |
| --------- | ----- |
|产品名称|SQL Server|  
|事件 ID|270|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|获取本地化的错误消息时出错。 “语言 ID”参数指定的语言未知。|  
  
## <a name="explanation"></a>说明  
 本地数据库运行时错误消息的请求的语言未知或不受支持。  
  
## <a name="user-action"></a>用户操作  
 尝试请求本地数据库运行时错误消息的支持的语言之一，或尝试请求默认语言。  
  
  
