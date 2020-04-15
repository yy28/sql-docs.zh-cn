---
title: SET 独占命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d140c4be3ab850547ac82f9b954e7313b008dbf0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300857"
---
# <a name="set-exclusive-command"></a>SET EXCLUSIVE 命令
指定表文件是打开，以便在网络上独占用途还是共享用途。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 将在网络上打开的表的可访问性限制为打开该表的用户。 网络上的其他用户无法访问该表。 设置独存打开还阻止所有其他用户具有只读访问权限。  
  
 OFF  
 （驱动程序默认值;Visual FoxPro 的默认值为全局数据会话为"打开"，对于私有数据会话为 OFF。允许网络上的任何用户共享和修改在网络上打开的表。  
  
## <a name="remarks"></a>备注  
 更改 SET EXCLUSIVE 的设置不会更改以前打开的表的状态。 例如，如果将具有 SET 独占集的表打开，然后将 SET 独占更改为 OFF，则该表将保留其独占使用状态。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
