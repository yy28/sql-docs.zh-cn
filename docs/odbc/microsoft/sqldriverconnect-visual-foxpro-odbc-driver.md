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
ms.openlocfilehash: c6fd8f3be1213a91195cd74a8b723629e2c5833f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053887"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：级别 1  
  
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
|描述||  
|排他|"是"或者"No"|  
|SourceDB|到一个目录，其中包含零个或更多的完全限定的路径[免费表](../../odbc/microsoft/visual-foxpro-terminology.md)，或为的绝对路径和文件名称[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)。|  
|SourceType|"DBC"或者"DBF"|  
|Version||  
  
 如果未指定数据源名称，驱动程序管理器会提示用户输入的信息 (具体取决于设置*fDriverCompletion*参数)，然后继续。 如果需要详细信息，Visual FoxPro ODBC 驱动程序将显示提示对话框。  
  
 有关详细信息，请参阅[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)中*ODBC 程序员参考*。
