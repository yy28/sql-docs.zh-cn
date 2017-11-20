---
title: "SQLConfigDataSource （文本文件驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e781871cc8507d10617e1a147fa6d5a7c06ac756
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource （文本文件驱动程序）
> [!NOTE]  
>  本主题提供文本文件特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函数，用于添加、 修改或删除数据源动态使用下列关键字。  
  
|关键字|Description|  
|-------------|-----------------|  
|CHARACTERSET|对于文本驱动程序中，OEM 或 ANSI。|  
|COLNAMEHEADER|对于文本驱动程序，该值指示数据的第一个记录是否将指定的列名称。 TRUE 或 FALSE。|  
|DEFAULTDIR|所指定的路径的目录。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置为相同的选项**说明**在安装程序对话框中。|  
|DRIVER|到驱动程序 DLL 路径规范。|  
|DRIVERID|驱动程序的整数 ID。 27 （文本）|  
|扩展|列出数据源上的文本文件的文件扩展名。<br /><br /> 这将设置为相同的选项**扩展列表**在安装程序对话框中。|  
|FIL|文件类型文本|  
|文件类型|文本驱动程序 （文本） 的文件类型。|  
|FORMAT|对于文本驱动程序，可以是 FIXEDLENGTH、 TABDELIMITED、 CSVDELIMITED （用逗号） 或 DELIMITED() （通过在括号中指定的特殊字符）。 特殊字符是一个字符的长度，并且可以是字符，十进制或十六进制格式。|  
|MAXSCANROWS|要设置基于现有数据的列的数据类型时扫描的行数。<br /><br /> 文本驱动程序，你可以输入一个介于 1 到 32767 之间的要扫描; 的行数但是，此值将始终默认为 25。 （限制以外的数字将返回错误。）<br /><br /> 这将设置为相同的选项**扫描的行数**在安装程序对话框中。|  
|READONLY|若要使文件成为只读的;如果为 FALSE，以使文件不是只读的。<br /><br /> 这将设置为相同的选项**Read Only**在安装程序对话框中。|

