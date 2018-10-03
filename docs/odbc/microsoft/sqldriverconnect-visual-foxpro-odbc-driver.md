---
title: SQLDriverConnect （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc0bcf6a191f67b87b422b17778f56feda1f5227
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792715"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 1  
  
 连接到现有的数据源，可以是[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)，或者的目录[免费表](../../odbc/microsoft/visual-foxpro-terminology.md)。 ODBC 属性关键字 UID 和 PWD 将被忽略。 下表列出了其他受支持的属性关键字。  
  
|ODBC 属性关键字|属性值|  
|----------------------------|---------------------|  
|DSN||  
|UID|Visual FoxPro ODBC 驱动程序被忽略，但不会生成错误。|  
|PWD|Visual FoxPro ODBC 驱动程序被忽略，但不会生成错误。|  
|驱动程序|名称和位置的 Visual FoxPro ODBC 驱动程序;实现由驱动程序管理器。|  
  
|Visual FoxPro ODBC 驱动程序属性关键字|属性值|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"是"或者"No"|  
|逐份打印|"计算机"或其他排序序列。 有关受支持的排序规则序列的列表，请参阅[设置 COLLATE](../../odbc/microsoft/set-collate-command.md)。|  
|Description||  
|排他|"是"或者"No"|  
|SourceDB|到一个目录，其中包含零个或更多的完全限定的路径[免费表](../../odbc/microsoft/visual-foxpro-terminology.md)，或为的绝对路径和文件名称[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)。|  
|SourceType|"DBC"或者"DBF"|  
|版本||  
  
 如果未指定数据源名称，驱动程序管理器会提示用户输入的信息 (具体取决于设置*fDriverCompletion*参数)，然后继续。 如果需要详细信息，Visual FoxPro ODBC 驱动程序将显示提示对话框。  
  
 有关详细信息，请参阅[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)中*ODBC 程序员参考*。
