---
title: MSSQLSERVER_33129 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b879bcb492783eec2cbca121f2596d096e2f673f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128558"
---
# <a name="mssqlserver33129"></a>MSSQLSERVER_33129
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|33129|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_CANNOT_DISABLE_WIN_GROUP|  
|消息正文|不能使用带 DISABLE 参数的 ALTER_LOGIN 来拒绝对 Windows 组的访问。|  
  
## <a name="explanation"></a>解释  
 尝试禁用某一 Windows 组的登录名时，会出现此消息。  
  
## <a name="user-action"></a>用户操作  
 Windows 组的登录名不能禁用。 若要暂时删除对某一 Windows 组授予的访问权限，则使用 REVOKE 命令吊销对 Windows 组的该登录名的 CONNECT 权限。 Windows 用户仍可能通过其单独的登录名或通过另一个 Windows 组具有访问权限。 下面的示例吊销 WESTCOAST 域的 Accounting 组的连接权限。  
  
```tsql  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
  