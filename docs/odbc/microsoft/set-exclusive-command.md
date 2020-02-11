---
title: 设置独占命令 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071761"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 命令
指定是否为在网络上以独占方式或共享方式打开表文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 限制在网络上打开的表对打开它的用户的可访问性。 网络上的其他用户无法访问此表。 设置 "独占" 还会阻止所有其他用户具有只读访问权限。  
  
 OFF  
 （驱动程序的默认值; 对于全局数据会话，Visual FoxPro 的默认值为 ON，对于专用数据会话，默认为关闭。）允许网络上的任何用户共享和修改在网络上打开的表。  
  
## <a name="remarks"></a>备注  
 更改 SET EXCLUSIVE 的设置不会更改以前打开的表的状态。 例如，如果在 "设置为" 设置为 "开" 的情况下打开表，并将 "独占" 设置为 "关"，则该表将保留其独占使用状态。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
