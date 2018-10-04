---
title: dbo.syscategories (Transact SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ee0509469f7a9bddca066a6e05416a13685ad9e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703515"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用于组织作业、警报和操作员的类别。 此表存储中**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|类别的 ID|  
|**category_class**|**int**|类别中的项目类型：<br /><br /> **1** = Job<br /><br /> **2** = 警报<br /><br /> **3** = 运算符|  
|**category_type**|**tinyint**|类别的类型：<br /><br /> **1** = 本地<br /><br /> **2** = 多服务器<br /><br /> **3** = 无|  
|**名称**|**sysname**|类别的名称|  
  
  
