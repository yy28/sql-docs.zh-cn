---
title: MSSQLSERVER_2508 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2508 (Database Engine error)
ms.assetid: c37d40e5-c665-4d66-a727-5cb845634fcc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7b09fcbc5e6e291ae87945d55bc534a0a63fb0c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62869154"
---
# <a name="mssqlserver2508"></a>MSSQLSERVER_2508
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2508|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_OUT_OF_DATE_PAGE_OR_ROW_COUNT|  
|消息正文|具有以下属性的对象的 %.*ls 计数不正确: 对象 "%.\*ls"、索引 ID %d、分区 ID %I64d、分配单元 ID %I64d (类型 %.\*ls)。 请运行 DBCC UPDATEUSAGE。|  
  
## <a name="explanation"></a>解释  
在版本低于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，用于表和索引行计数以及页计数的值可能不正确。 根据 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前的版本创建的数据库可能包含错误的计数。 已经对 DBCC CHECKDB 进行了增强，可以检测这些错误并在遇到错误时返回此警告消息。  
  
## <a name="user-action"></a>用户操作  
请针对指定的对象或索引或者针对包含该对象的数据库运行 DBCC UPDATEUSAGE，以更正无效计数。  
  
