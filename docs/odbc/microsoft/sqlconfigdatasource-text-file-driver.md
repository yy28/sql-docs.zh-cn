---
title: SQLConfigDataSource （文本文件驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46bb00fb01ed3fee8098420794af089f2d8b981e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054083"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 用于动态添加、修改或删除数据源的**SQLConfigDataSource**函数使用以下关键字。  
  
|关键字|说明|  
|-------------|-----------------|  
|CHARACTERSET|对于文本驱动程序，OEM 或 ANSI。|  
|COLNAMEHEADER|对于文本驱动程序，指示数据的第一个记录是否将指定列名称。 TRUE 或 FALSE。|  
|DEFAULTDIR|目录的路径规范。|  
|说明|数据源中数据的说明。<br /><br /> 这会在 "设置" 对话框中设置与 "**描述**" 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|DRIVERID|驱动程序的整数 ID。 27（文本）|  
|扩展名|列出数据源上的文本文件的文件扩展名。<br /><br /> 这会设置与 "设置" 对话框中的 "**扩展" 列表**相同的选项。|  
|FIL|文件类型文本|  
|FILETYPE|文本驱动程序的文件类型（文本）。|  
|FORMAT|对于文本驱动程序，可以是 FIXEDLENGTH、TABDELIMITED、CSVDELIMITED （用逗号分隔），也可以是分隔的（）（通过括号中指定的特殊字符）。 特殊字符的长度为一个字符，可以是字符、十进制或十六进制格式。|  
|MAXSCANROWS|基于现有数据设置列的数据类型时要扫描的行数。<br /><br /> 对于文本驱动程序，可以为要扫描的行数输入1到32767之间的一个数字;但是，值始终默认为25。 （超出限制的数字将返回错误。）<br /><br /> 这会在 "安装程序" 对话框中设置与**要扫描的行**相同的选项。|  
|READONLY|若要使文件为只读，则为 TRUE;如果设置为 FALSE，则使文件不为只读。<br /><br /> 这会在 "设置" 对话框中设置与 "**只读**" 相同的选项。|
