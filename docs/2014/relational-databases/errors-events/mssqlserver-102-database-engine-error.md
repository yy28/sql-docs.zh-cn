---
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee88ba8a77602fd50412669f96e1e16ddcdd37c7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203937"
---
# <a name="mssqlserver102"></a>MSSQLSERVER_102
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|102|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|P_SYNTAXERR2|  
|消息正文|“%.*ls”附近有语法错误。|  
  
## <a name="explanation"></a>解释  
 指示语法错误。 无法提供其他信息，因为该错误阻止[!INCLUDE[ssDE](../../includes/ssde-md.md)]处理语句。  
  
 当不处于 90 或 100 兼容模式下时，如果尝试使用不推荐使用的 RC4 或 RC4_128 加密创建对称密钥，可能导致此错误。  
  
## <a name="user-action"></a>用户操作  
 搜索 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，查找语法错误。  
  
 如果使用 RC4 或 RC4_128 创建对称密钥，请选择较新的加密（如某个 AES 算法）。 （建议。）如果必须使用 RC4，请使用 ALTER DATABASE SET COMPATIBILITY_LEVEL 将数据库兼容级别设置为 90 或 100。 （建议不要使用。）  
  
  
