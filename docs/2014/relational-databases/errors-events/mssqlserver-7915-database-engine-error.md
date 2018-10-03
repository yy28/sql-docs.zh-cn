---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb60bfa05e75c06b7da04042aa1abfbd42b756c0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48109027"
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7915|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|消息正文|修复: 对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID，分配单元 ID A_ID（类型为 TYPE）的 IAM 链已在页 P_ID 前截断，将重新生成该链。|  
  
## <a name="explanation"></a>解释  
 这是 REPAIR 发送的信息性消息，指示修补了指定的索引分配映射 (IAM) 链，以便可以重新生成它。 此修补可能需要分配新的 IAM 链头或者删除错误页。  
  
## <a name="user-action"></a>用户操作  
 None  
  
  
