---
title: “服务器触发器递归”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- recursive triggers [SQL Server]
- triggers [SQL Server], recursive
- server trigger recursion option
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 23a4997bd1a6f8b2c04af34d5cdc3229575901a9
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934849"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>server trigger recursion 服务器配置选项
  使用 **server trigger recursion** 选项可指定是否允许服务器级触发器递归激发。 当此选项设置为 1 (ON) 时，将允许服务器级触发器递归激发。 当设置为 0 (OFF) 时，服务器级触发器不能递归激发。 当 server trigger recursion 选项设置为 0 (OFF) 时，仅阻止直接递归。 （若要禁用间接递归，请将 **nested triggers** 选项设置为 0。）该选项的默认值为 1 (ON)。 该设置更改后立即生效，而不需要重新启动服务器。  
  
 有关详细信息，请参阅 [创建嵌套触发器](../../relational-databases/triggers/create-nested-triggers.md)。  
  
## <a name="see-also"></a>另请参阅  
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
