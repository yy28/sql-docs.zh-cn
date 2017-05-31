---
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4184a493ecfcb3d22c8e6e6fdd93b8e9fe756a9
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

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
  

