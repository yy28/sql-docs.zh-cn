---
title: 设置 COLLATE 命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a9c1dfd59c00ad0ac0b7bd8b8f1cdfccc84d9b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300887"
---
# <a name="set-collate-command"></a>SET COLLATE 命令
为后续索引和排序操作中字符字段指定排序序列。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>参数  
 *c序列名称*  
 指定排序规则序列。 下表描述了可用的排序规则选项。  
  
|选项|语言|  
|-------------|--------------|  
|荷兰语|荷兰语|  
|GENERAL|英语、法语、德语、现代西班牙语、葡萄牙语和其他西欧语言|  
|德语|德国电话簿订单 （DIN）|  
|冰岛|冰岛语|  
|机|计算机（早期 FoxPro 版本的默认排序规则序列）|  
|诺丹|挪威语， 丹麦语|  
|西班牙语|传统西班牙语|  
|斯威芬|瑞典语， 芬兰语|  
|优衣库|独特的重量|  
  
> [!NOTE]  
>  指定 SPANISH 选项时 *，ch*是一个字母，在*c*和*d*之间排序，*并在* *l*和*m*之间排序。  
  
 如果将排序规则序列选项指定为文本字符串，请确保在引号中包含该选项：  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MACHINE 是默认排序规则序列选项，是 Xbase 用户熟悉的序列。 字符在当前代码页中显示时进行排序。  
  
 对于美国和西欧用户来说，GENERAL 可能更可取。 字符在当前代码页中显示时进行排序。 在 FoxPro 版本早于 2.5 中，索引可能已使用**上部**（ ） 或**LOWER**（ ） 函数创建，以将字符字段转换为一致大小写。 在 FoxPro 版本晚于 2.5 中，您可以改为指定 GENERAL 排序规则序列选项并省略**UPPER**（ ） 转换。  
  
 如果指定"机器"以外的排序规则序列选项，并且如果创建 .idx 文件，则始终创建紧凑的 .idx。  
  
 使用 SET（"COLLATE"）返回当前排序规则序列。  
  
 您可以使用[ODBC 可视化 FoxPro 安装程序对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)或使用与[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)的连接字符串中的"Collate 关键字"为数据源指定整理序列。 这与发出以下命令相同：  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>备注  
 SET COLLATE 使您能够为任何受支持的语言订购包含重音字符的表。 更改 SET COLLATE 的设置不会影响以前打开的索引的整理顺序。 Visual FoxPro 可自动维护现有索引，从而灵活地创建许多不同类型的索引，即使对于同一字段也是如此。  
  
 例如，如果使用 SET COLLATE 设置为"GENERAL"创建索引，并且"设置 COLLATE"设置稍后更改为西班牙语，则索引将保留"常规排序规则"序列。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
