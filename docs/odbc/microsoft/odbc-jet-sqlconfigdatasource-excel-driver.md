---
title: ODBC 喷气 SQLConfigData 来源（Excel 驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293007"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource（Excel 驱动程序）
> [!NOTE]  
>  本主题提供特定于 Excel 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLConfigDataSource**函数用于动态添加、修改或删除数据源，使用以下关键字。  
  
|关键字|描述|  
|-------------|-----------------|  
|DBQ|对于访问 Microsoft Excel 5.0 或更高版本文件时的 Microsoft Excel 驱动程序，工作簿文件的名称。<br /><br /> 这将在设置对话框中设置与**数据库**相同的选项。|  
|默认DIR|目录的路径规范。<br /><br /> 这将设置与设置对话框中的 **"选择目录"** 或 **"选择工作簿"** 相同的选项。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置与设置对话框中的 **"说明"** 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|驱动程序 ID|驱动程序的整数 ID。<br /><br /> 534 （微软 Excel 3.0）<br /><br /> 278 （微软 Excel 4.0）<br /><br /> 22 （微软 Excel 5.0/7.0）<br /><br /> 790 （微软 Excel 97-2003）|  
|FIL|文件类型，例如 Excel 3.0、Excel 4.0、Excel 5.0、Excel 7.0、Excel 97、Excel 2000 或 Excel 2003。|  
|第一罗哈斯名称|指示区域第一行的单元格是否包含表 （1） 的列名称 （0）。|  
|马克斯坎罗斯|根据现有数据设置列的数据类型时要扫描的行数。<br /><br /> 可以输入从 1 到 16 的数字来扫描行。 该值默认为 8;如果设置为 0，则扫描所有行。 （超出限制的数字将返回错误。<br /><br /> 这将在设置对话框中设置与 **"要扫描的行"** 相同的选项。|  
|READONLY|TRUE 使文件为只读;FALSE 使文件不只读。<br /><br /> 这将在设置对话框中设置与 **"只读"** 相同的选项。|  
|线程|发动机要使用的后台线程数。 对于 Microsoft Access 驱动程序，此值默认为 3，但可以更改。 对于 dBASE，MicrosoftExcel 驱动程序此值为 3，不能更改。<br /><br /> 这将设置与设置对话框中的 **"线程"** 相同的选项。|
