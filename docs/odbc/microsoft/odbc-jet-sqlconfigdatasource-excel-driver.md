---
title: ODBC Jet SQLConfigDataSource （Excel 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a76482acd1182d900336d7ac9826b16968e00caa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293007"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 用于动态添加、修改或删除数据源的**SQLConfigDataSource**函数使用以下关键字。  
  
|关键字|说明|  
|-------------|-----------------|  
|DBQ|在访问 Microsoft Excel 5.0 或更高版本的文件时，为 Microsoft Excel 驱动程序提供工作簿文件的名称。<br /><br /> 这会在 "设置" 对话框中设置与**数据库**相同的选项。|  
|DEFAULTDIR|目录的路径规范。<br /><br /> 这会在 "安装程序" 对话框中设置与 "**选择目录**" 或**选择 "工作簿**" 相同的选项。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这会在 "设置" 对话框中设置与 "**描述**" 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|DRIVERID|驱动程序的整数 ID。<br /><br /> 534（Microsoft Excel 3.0）<br /><br /> 278（Microsoft Excel 4.0）<br /><br /> 22（Microsoft Excel 5.0/7.0）<br /><br /> 790（Microsoft Excel 97-2003）|  
|FIL|文件类型，例如 Excel 3.0、Excel 4.0、Excel 5.0、Excel 7.0、Excel 97、Excel 2000 或 Excel 2003。|  
|FIRSTROWHASNAMES|指示范围中第一行的单元格是否包含表的列名称（1）或不包含（0）。|  
|MAXSCANROWS|基于现有数据设置列的数据类型时要扫描的行数。<br /><br /> 可以为要扫描的行输入一个介于1到16之间的数字。 该值默认为 8;如果设置为0，则扫描所有行。 （超出限制的数字将返回错误。）<br /><br /> 这会在 "安装程序" 对话框中设置与**要扫描的行**相同的选项。|  
|READONLY|若要使文件为只读，则为 TRUE;如果设置为 FALSE，则使文件不为只读。<br /><br /> 这会在 "设置" 对话框中设置与 "**只读**" 相同的选项。|  
|线程|引擎要使用的后台线程数。 对于 Microsoft Access 驱动程序，此值默认为3，但可以更改。 对于 dBASE，MicrosoftExceldriver 此值为3，并且无法更改。<br /><br /> 这会设置与 "设置" 对话框中的**线程**相同的选项。|
