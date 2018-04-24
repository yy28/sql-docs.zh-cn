---
title: MSSQLSERVER_7711 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7711 (Database Engine error)
ms.assetid: a5c7cd6e-18d6-47ef-902b-db9dd64bba34
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f75bef86a606da4f7103c3afd6c5846dc58e8e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7711"></a>MSSQLSERVER_7711
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7711|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PRT_RANGE_OVERLAP|  
|消息正文|为表或索引或其中一个分区多次指定了 DATA_COMPRESSION 选项。|  
  
## <a name="explanation"></a>解释  
以下语句之一中的 DATA_COMPRESSION 选项出错：  
  
-   CREATE TABLE  
  
-   ALTER TABLE  
  
-   CREATE INDEX  
  
-   ALTER INDEX  
  
如果引用的表或索引已分区，则 DATA_COMPRESSION 选项对其中至少一个分区列出了不止一次。 如果表或索引未分区，则不止一次引用了 DATA_COMPRESSION 选项。  
  
## <a name="user-action"></a>用户操作  
对于已分区表或已分区索引，请确保仅对每个分区指定一次 DATA_COMPRESSION 选项。 对于未分区的表或索引，请在语句中仅使用一次 DATA_COMPRESSION 选项。  
  
