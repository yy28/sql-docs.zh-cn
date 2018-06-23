---
title: LOCALDB_ERROR_NOT_INSTALLED |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e7912885-1c14-409b-9022-83ad4c36f3bd
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 730a6ce39b1711897dc77ca16e54722c7b9d1f47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017321"
---
# <a name="localdberrornotinstalled"></a>LOCALDB_ERROR_NOT_INSTALLED
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|278|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|**注意：** 消息文本为空，因为此消息意味着整个 LocalDB API （包括将 HRESULT 映射到消息文本的 FormatMessage 函数） 不可用。|  
  
## <a name="explanation"></a>解释  
 计算机上没有安装本地数据库运行时。  
  
## <a name="user-action"></a>用户操作  
 安装本地数据库运行时，然后重试操作。  
  
  