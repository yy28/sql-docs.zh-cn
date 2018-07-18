---
title: MSSQLSERVER_7914 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7914 (Database Engine error)
ms.assetid: d32a81ce-4ca7-4b33-b536-c7ea0ed6f226
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ad252c6f77117c19918d76cae11a5630f69d3e40
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34324913"
---
# <a name="mssqlserver7914"></a>MSSQLSERVER_7914
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7914|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_ALLOCATION_PAGE_REBUILT|  
|消息正文|修复: 位于 P_ID 的 PAGE_TYPE 页已重新生成。|  
  
## <a name="explanation"></a>解释  
这是来自 REPAIR 的信息性消息，该消息声明 GAM 或 SGAM 页已通过使用 PFS 页数据重新生成。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
