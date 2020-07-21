---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 31953e9f8cef351819d5b1cd47195e9bf9308738
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551102"
---
# <a name="mssqlserver_617"></a>MSSQLSERVER_617
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|617|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NODESHASH|  
|消息正文|尝试对数据库 ID %d 中的对象 ID %ld 的描述符进行解哈希运算时，在哈希表中没有找到该描述符。 工作表缺少条目。 请重新运行查询。 如果涉及到游标，请关闭游标，然后重新打开。|  
  
## <a name="explanation"></a>说明  
 SQL Server 在工作表中找不到特定项。  
  
## <a name="user-action"></a>用户操作  
  
1.  如果涉及到游标，请关闭游标，然后重新打开。  
  
2.  再次运行查询。  
  
  
