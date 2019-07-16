---
title: SET EXCLUSIVE 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d1a37043d332b54d0d5c5ebb7b2ba9f3acce000
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071761"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 命令
指定是否为独占或共享网络上打开表的文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 打开到打开它的用户在网络上的表的限制可访问性。 表不是在网络上其他用户访问。 SET 独占 ON 还可防止其他用户拥有只读访问权限。  
  
 OFF  
 （默认为驱动程序; Visual FoxPro 的默认值为专用数据会话的全局数据会话和 OFF 为 ON。）允许打开网络共享并在网络上的任何用户修改上一个表。  
  
## <a name="remarks"></a>备注  
 更改设置排他的设置不会更改以前打开的表的状态。 例如，如果与设置排他设置为开打开表，并设置排他随后更改为 OFF，表将保留其独占使用状态。  
  
## <a name="see-also"></a>请参阅  
 [ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
