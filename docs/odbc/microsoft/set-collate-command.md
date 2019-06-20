---
title: SET COLLATE 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 372d3b2df79d66084f5599b4ac098b8c273ee78a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127834"
---
# <a name="set-collate-command"></a>SET COLLATE 命令
在后续索引和排序操作中指定字符字段的排序规则的顺序。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>参数  
 *cSequenceName*  
 指定排序规则顺序。 下表所述的可用排序规则序列选项。  
  
|选项|语言|  
|-------------|--------------|  
|荷兰语|荷兰语|  
|GENERAL|英语、 法语、 德语、 现代西班牙语、 葡萄牙语、 和其他西欧语言|  
|德语|正使用德语电话簿顺序 (DIN)|  
|冰岛|冰岛语|  
|计算机|计算机 （默认排序规则顺序对于较早的 FoxPro 版本）|  
|NORDAN|挪威语、 丹麦语|  
|西班牙语|传统西班牙语|  
|SWEFIN|瑞典语、 芬兰语|  
|UNIQWT|唯一的权重|  
  
> [!NOTE]  
>  当指定西班牙语选项， *ch*是一个之间进行排序的单个字母*c*和*d*，和*ll*之间进行排序*l*并*m*。  
  
 如果文本以字符串形式指定排序规则序列选项，请务必将用引号引起来：  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 计算机是默认排序规则序列选项，会序列 Xbase 用户非常熟悉。 当前代码页中的显示方式，是有序字符。  
  
 常规可能适用于美国和西欧语言用户更好。 当前代码页中的显示方式，是有序字符。 在 FoxPro 版本早于 2.5 中，索引可能已创建了使用**上部**（) 或**低**（） 函数将字符字段转换为大小写一致。 在晚于 2.5 FoxPro 版本中，可以改为指定的常规排序规则序列选项，并省略**上部**（） 转换。  
  
 如果指定的排序规则序列选项机和创建.idx 文件以外，compact.idx 始终会创建。  
  
 使用 SET("COLLATE") 返回当前的排序规则顺序。  
  
 可以通过使用指定的数据源的排序规则序列[ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或通过使用在连接字符串中使用 Collate 关键字[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。 这等同于发出以下命令：  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>备注  
 设置排序规则可以包含带重音的字符的任何支持的语言的订单表。 更改设置排序规则的设置不会影响以前打开的索引的排序顺序。 Visual FoxPro 自动维护现有索引，提供灵活地创建许多不同类型的索引，即使对于同一个字段。  
  
 例如，如果设置排序规则设置为常规使用创建索引并设置排序规则设置之后更改为西班牙语，索引将保留的常规排序规则顺序。  
  
## <a name="see-also"></a>请参阅  
 [ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
