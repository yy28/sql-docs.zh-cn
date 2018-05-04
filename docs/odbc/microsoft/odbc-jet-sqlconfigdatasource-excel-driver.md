---
title: ODBC Jet SQLConfigDataSource （Excel 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00b2295ead09d0196a14248b03ee5f6a96936df6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource （Excel 驱动程序）
> [!NOTE]  
>  本主题提供 Excel 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函数，用于添加、 修改或删除数据源动态使用下列关键字。  
  
|关键字|Description|  
|-------------|-----------------|  
|DBQ|Microsoft Excel 驱动程序访问 Microsoft Excel 5.0 或更高版本的文件时的工作簿文件的名称。<br /><br /> 这将设置为相同的选项**数据库**在安装程序对话框中。|  
|DEFAULTDIR|所指定的路径的目录。<br /><br /> 这将设置为相同的选项**选择目录**或**选择工作簿**在安装程序对话框中。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置为相同的选项**说明**在安装程序对话框中。|  
|DRIVER|到驱动程序 DLL 路径规范。|  
|DRIVERID|驱动程序的整数 ID。<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|文件类型，例如，Excel 3.0、 Excel 4.0、 Excel 5.0、 Excel 7.0，Excel 97、 Excel 2000 或 Excel 2003。|  
|FIRSTROWHASNAMES|表示范围的第一行的单元格是否包含表 (1) 的列名称，或不 (0)。|  
|MAXSCANROWS|要设置基于现有数据的列的数据类型时扫描的行数。<br /><br /> 可以为要扫描的行输入一个介于 1 到 16。 默认值为 8;如果设置为 0，将扫描所有行。 （限制以外的数字将返回错误。）<br /><br /> 这将设置为相同的选项**扫描的行数**在安装程序对话框中。|  
|READONLY|若要使文件成为只读的;如果为 FALSE，以使文件不是只读的。<br /><br /> 这将设置为相同的选项**Read Only**在安装程序对话框中。|  
|线程|要使用的引擎的后台线程数。 对于 Microsoft Access 驱动程序，此值默认为 3，但可以更改。 为 dBASE，MicrosoftExceldriver 此值为 3，而不能更改。<br /><br /> 这将设置为相同的选项**线程**在安装程序对话框中。|
