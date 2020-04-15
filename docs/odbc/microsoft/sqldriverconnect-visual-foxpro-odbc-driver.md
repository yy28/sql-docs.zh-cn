---
title: SQLDriverConnect（可视化福克斯Pro ODBC驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e270f8c9be42dc109adeaa49acb84f29f2b9511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307088"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 符合性：1 级  
  
 连接到现有数据源，数据源可以是[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)或[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录。 ODBC 属性关键字 UID 和 PWD 将被忽略。 下表列出了其他受支持的属性关键字。  
  
|ODBC 属性关键字|属性值|  
|----------------------------|---------------------|  
|DSN||  
|UID|被 Visual FoxPro ODBC 驱动程序忽略，但不会生成错误。|  
|PWD|被 Visual FoxPro ODBC 驱动程序忽略，但不会生成错误。|  
|驱动程序|视觉福克斯Pro ODBC驱动程序的名称和位置;由驱动程序管理器实施。|  
  
|可视化福克斯Pro ODBC驱动程序属性关键字|属性值|  
|-------------------------------------------------|---------------------|  
|背景提取|"是"或"否"|  
|逐份打印|"机器"或其他整理序列。 有关支持的整理序列的列表，请参阅[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。|  
|描述||  
|排他|"是"或"否"|  
|SourceDB|包含零个或多个[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录的完全限定路径，或[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的绝对路径和文件名。|  
|SourceType|"DBC"或"DBF"|  
|版本||  
  
 如果未指定数据源名称，驱动程序管理器会提示用户提供信息（取决于*fDriver 完成*参数的设置），然后继续。 如果需要更多信息，可视化 FoxPro ODBC 驱动程序将显示提示对话框。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLDriverConnect。](../../odbc/reference/syntax/sqldriverconnect-function.md)
