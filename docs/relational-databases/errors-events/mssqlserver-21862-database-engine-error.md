---
title: MSSQLSERVER_21862 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f2dce4f256ca0bed1da86a6205e18e04c341f52
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34321228"
---
# <a name="mssqlserver21862"></a>MSSQLSERVER_21862
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|21862|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21862|  
|消息正文|无法使用同步方法 'database snapshot' 或 'database snapshot character' 在发布中发布 FILESTREAM 列。|  
  
## <a name="explanation"></a>解释  
由于无法通过数据库快照访问 FILESTREAM 数据，因此，为发布的同步方法指定 *database snapshot* 或 *database_snapshot_character* 参数时，快照代理将无法读取 FILESTREAM 数据。  
  
## <a name="user-action"></a>用户操作  
将发布的同步方法更改为 *database snapshot* 或 *database_snapshot_character* 以外的参数，或者只是在发布中排除 FILESTREAM 列。  
  
