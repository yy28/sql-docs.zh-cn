---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14e593ef1dba6a6bed7c5d8a7a1fa42e642ee7d7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428366"
---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|10737|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|消息正文|在 ALTER TABLE REBUILD 或 ALTER INDEX REBUILD 语句中，如果在 DATA_COMPRESSION 语句中指定了一个分区，则必须指定 PARTITION=ALL。 PARTITION=ALL 子句用来强调表或索引的所有分区将重新生成，即使仅在 DATA_COMPRESSION 子句中指定了一个子集也是如此。|  
  
## <a name="user-action"></a>用户操作  
 将 PARTITION=ALL 子句添加到 ALTER TABLE 或 ALTER INDEX 语句中。 或者，若要重新生成特定分区，请使用 REBUILD PARTITION = \<partition-number-expr> WITH (DATA_COMPRESSION={ON | OFF})。  
  
  
