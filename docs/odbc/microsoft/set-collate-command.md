---
title: "SET COLLATE 命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 73bf988f0ab1b181a75c7569c8b279b36a9b76d8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="set-collate-command"></a>SET COLLATE 命令
在后续索引和排序操作中指定字符字段排序规则的序列。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>参数  
 *cSequenceName*  
 指定排序规则序列。 下表中描述了可用的排序规则序列选项。  
  
|选项|语言|  
|-------------|--------------|  
|荷兰语|荷兰语|  
|GENERAL|英语、 法语、 德语、 现代西班牙语、 葡萄牙语、 和其他西欧语言|  
|德语|德语电话薄顺序 (DIN)|  
|冰岛|冰岛语|  
|机|机 （默认排序规则序列的早期 FoxPro 版本）|  
|NORDAN|挪威语、 丹麦语|  
|西班牙语|传统西班牙语|  
|SWEFIN|瑞典语、 芬兰语|  
|UNIQWT|唯一的权重|  
  
> [!NOTE]  
>  如果指定西班牙语的选项， *ch*之间进行排序是一个字母*c*和*d*，和*ll*之间进行排序*l*和*m*。  
  
 如果文本字符串形式指定排序规则序列选项，请务必用引号引起来的选项：  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 机是默认排序规则序列选项，并处于序列 Xbase 用户熟悉。 在当前代码页中显示，字符进行排序。  
  
 常规可能优于美国和西欧用户。 在当前代码页中显示，字符进行排序。 在 FoxPro 版本早于 2.5 中，索引可能已使用创建了**上部**（) 或**较低**（） 函数将字符字段转换为一致的用例。 在晚于 2.5 FoxPro 版本中，可以改为指定的常规的排序规则序列选项，并省略**上部**（） 转换。  
  
 如果指定计算机和如果创建一个.idx 文件以外的排序规则序列选项时，始终会创建 compact.idx。  
  
 使用 SET("COLLATE") 返回当前的排序规则序列。  
  
 你可以通过使用指定的数据源的排序规则序列[ODBC Visual FoxPro 安装程序对话框中](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或在与连接字符串中使用 Collate 关键字[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)。 这等同于发出以下命令：  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>注释  
 设置 COLLATE 使您能够包含任何受支持的语言的重音的字符顺序表。 更改设置排序规则的设置不会影响先前已打开的索引的排序顺序。 Visual FoxPro 自动维护现有索引，提供可以灵活地创建许多不同类型的索引，即使为相同的字段。  
  
 例如，如果使用设置排序规则设置为常规创建索引，并且设置排序规则设置更高版本更改为西班牙语，索引将保留常规的排序规则序列。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
