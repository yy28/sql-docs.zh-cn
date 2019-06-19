---
title: 使用 Visual Basic 应用程序使用 VFP FoxPro ODBC 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b77fdee70ff73772710c9758eeb2bf2594f365d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280951"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>配合使用 VFP FoxPro ODBC 驱动程序和 Visual Basic 应用程序
你的 Microsoft® Visual Basic® 应用程序可以与 Visual FoxPro 数据通信通过创建连接到 Visual FoxPro 数据源的数据控件。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>若要连接到 Visual Basic 中使用的数据控件的 Visual FoxPro 数据  
  
1.  创建名为"test"的数据源连接到包含在 Visual FoxPro TasTrade 示例数据库。 默认 Visual FoxPro 安装位置中位置 TasTrade 示例数据库：  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  在 Visual Basic 中创建新的窗体并放置一个文本框和上的某个数据控件。  
  
3.  更改数据控件的连接属性，如下所示：  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  更改记录集类型属性设置为以下内容：  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  更改记录源属性设置为以下内容：  
  
    ```  
    customer  
    ```  
  
6.  将文本框中的数据源属性更改到以下的数据控件的默认名称为：  
  
    ```  
    data1  
    ```  
  
7.  将文本框的 DataField 属性更改为以下：  
  
    ```  
    customer_id  
    ```  
  
8.  运行该窗体，并使用数据控件从 Visual FoxPro TasTrade 示例数据库的客户 id 字段通过跳过。
