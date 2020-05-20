---
title: dbo. syscategories （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fc4d6f55ca4e131abef21772911da923b854c81b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813822"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用于组织作业、警报和操作员的类别。 该表存储在**msdb**数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|类别的 ID|  
|**category_class**|**int**|类别中的项目类型：<br /><br /> **1** = 作业<br /><br /> **2** = 警报<br /><br /> **3** = 运算符|  
|**category_type**|**tinyint**|类别的类型：<br /><br /> **1** = 本地<br /><br /> **2** = 多服务器<br /><br /> **3** = 无|  
|**name**|**sysname**|类别的名称|  
  
  
