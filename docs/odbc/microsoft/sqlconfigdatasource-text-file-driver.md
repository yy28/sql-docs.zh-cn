---
title: SQLConfigData 源（文本文件驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d2809f9b15dd6843e4404c7cf1887c3caa015a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283917"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLConfigDataSource**函数用于动态添加、修改或删除数据源，使用以下关键字。  
  
|关键字|描述|  
|-------------|-----------------|  
|字符集|对于文本驱动程序、OEM 或 ANSI。|  
|科尔纳梅头|对于 Text 驱动程序，指示第一个数据记录是否将指定列名称。 真或假。|  
|默认DIR|目录的路径规范。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置与设置对话框中的 **"说明"** 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|驱动程序 ID|驱动程序的整数 ID。 27 （文本）|  
|扩展|列出数据源上文本文件的文件名扩展名。<br /><br /> 这将在设置对话框中设置与**扩展列表**相同的选项。|  
|FIL|文件类型 文本|  
|文件类型|文本驱动程序（文本）的文件类型。|  
|FORMAT|对于文本驱动程序，可以是固定长度、TABDE限制、CSVDE限制（通过逗号）或 DELIMITED（通过括号中指定的特殊字符）。 特殊字符的长度是一个字符，可以是字符、十进制或十六进制格式。|  
|马克斯坎罗斯|根据现有数据设置列的数据类型时要扫描的行数。<br /><br /> 对于 Text 驱动程序，您可以输入从 1 到 32767 的数字，以便扫描的行数;但是，该值将始终默认为 25。 （超出限制的数字将返回错误。<br /><br /> 这将在设置对话框中设置与 **"要扫描的行"** 相同的选项。|  
|READONLY|TRUE 使文件为只读;FALSE 使文件不只读。<br /><br /> 这将在设置对话框中设置与 **"只读"** 相同的选项。|
