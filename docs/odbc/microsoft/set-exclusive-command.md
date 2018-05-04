---
title: SET 独占命令 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a5ab2ccf22c7322fa0e35cd281a8953b7685a02
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="set-exclusive-command"></a>SET 独占命令
指定是否在网络上独占或共享用于打开表文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 向打开它的用户的网络上打开一个表的限制可访问性。 表无法访问网络上的其他用户。 SET 独占 ON 还会阻止所有其他用户具有只读访问权限。  
  
 OFF  
 （默认驱动程序; Visual FoxPro 的默认值为私有数据会话的全局数据会话和 OFF 如下 ON）。允许在网络共享和在网络上的任何用户修改上打开一个表。  
  
## <a name="remarks"></a>注释  
 更改设置排他的设置不会更改以前打开表的状态。 例如，如果表将打开，其中设置独占设置为 ON 和独占设置更高版本更改为 OFF，表将保留其独占使用状态。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
