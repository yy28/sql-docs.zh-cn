---
title: 非系统区域设置 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- locale, linux, macOS, system
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: bd60bff3ab9ee19b1a1d2435e69651ea054689e7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "76913320"
---
# <a name="non-system-locale-settings"></a>非系统区域设置
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本部分仅适用于 Linux 和 macOS 用户，尤其是在其 php 应用程序中处理多个区域设置的用户。

默认情况下，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 采用系统中定义的 `LC_ALL` 环境变量，并重写所有其他 `LC_xxx` 类别（某些情况下 `$LANG` 或 `$LANGUAGE` 可能除外），这会影响千位分隔符、小数点字符、字符集、月份、日期名称、应用程序消息（如错误消息）、货币符号等。

从版本 5.8.0 开始，用户可以使用 php.ini 文件配置本地化设置，如以下示例所示。

## <a name="set-locale-info-using-the-sqlsrv-driver"></a>使用 SQLSRV 驱动程序设置区域设置信息  
在 php.ini 文件末尾添加以下内容：
  
```  
[sqlsrv]  
sqlsrv.SetLocaleInfo = <option>
```  
  
## <a name="set-locale-info-using-the-pdo_sqlsrv-driver"></a>使用 PDO_SQLSRV 驱动程序设置区域设置信息  
在 php.ini 文件末尾添加以下内容：
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.set_locale_info = <option>
```  
  
选项  可以是下列值之一：  
  
|选项|行为说明|
|---------|---------------|
|0|驱动程序将忽略系统区域设置。|
|1|驱动程序读取 LC_CTYPE 变量。|
|2|驱动程序读取 LC_ALL 变量（这是默认值）。|
  

`LC_CTYPE` 类别确定字符处理规则，这些规则控制文本数据字符字节序列的解释、字符分类以及字符类的行为。 它控制大写和小写、字母和非字母字符等的识别。

### <a name="explanation"></a>说明

1. 选项 0 -- 如果不想更改应用程序区域设置，请使用此选项。

1. 选项 1 -- 仅用于设置 `LC_CTYPE` 的系统值，而不影响其他 `LC_xxx` 类别。

1. 选项 2 -- 使用 `LC_ALL` 重写所有 `LC_xxx` 类别，这会影响 php 应用程序及其扩展。

如果任何 php 脚本的区域设置与系统不同，则可能需要通过调用 php 内置函数 [setlocale](https://www.php.net/manual/en/function.setlocale.php) 来指定 php 脚本中的区域设置。 

例如，如果系统默认值为 `en_US.UTF-8` 但 php 脚本使用 `de_DE.UTF-8`，则相应地调用 php 函数 `setlocale()`。

对于选项 2，仅当 php 脚本中的所需区域设置与 `LC_ALL` 变量不同时，才指示该区域设置。

> [!NOTE]
> 如果在 php.ini 中未定义任何内容，则当前默认设置将基于 `LC_ALL` 重写所有其他区域设置，这些设置将被弃用  。 在不久的将来，默认设置将忽略系统区域设置。 因此，如果用户想要保留当前行为，他们将需要相应地修改 php.ini 文件。

如果同时启用 sqlsrv 和 pdo_sqlsrv 驱动程序，则不建议为这两个驱动程序设置不同的选项。