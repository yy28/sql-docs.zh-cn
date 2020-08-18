---
description: MSSQLSERVER_15661
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1f851c38ab44e84fa6afd21374c2b2d2680187a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88333263"
---
# <a name="mssqlserver_15661"></a>MSSQLSERVER_15661
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|15661|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum15661|  
|消息正文|sp_estimate_data_compression_savings 存储过程不能用于临时表。|  
  
## <a name="explanation"></a>说明  
临时表已用作 sp_estimate_data_compression_savings 存储过程的参数。 尽管支持压缩临时表，但 sp_estimate_data_compression_savings 不能用于估计压缩的存储内容。  
  
## <a name="user-action"></a>用户操作  
删除用作 sp_estimate_data_compression_savings 参数的临时表。  
  
