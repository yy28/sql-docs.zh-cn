---
title: "使用 Visual Basic 应用程序的 VFP FoxPro ODBC 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 37834afc7cc69e0276645d68752e66f68449fbb3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>使用 Visual Basic 应用程序的 VFP FoxPro ODBC 驱动程序
通过创建一个数据控件，连接到 Visual FoxPro 数据源时，你的 Microsoft® Visual Basic® 应用程序可以与 Visual FoxPro 数据通信。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>若要连接到 Visual FoxPro 数据使用 Visual Basic 中的数据控件  
  
1.  创建名为"test"的数据源连接到 Visual FoxPro 中包含的 TasTrade 示例数据库。 默认 Visual FoxPro 安装在位置放置 TasTrade 示例数据库：  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  在 Visual Basic 中，创建一个新的窗体和放置一个文本框和在其上的一个数据控件。  
  
3.  更改该数据控件的连接属性，如下所示：  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  将记录集类型属性更改为以下：  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  将记录源属性更改为以下：  
  
    ```  
    customer  
    ```  
  
6.  将文本框中的数据源属性更改为以下数据控件的默认名称为：  
  
    ```  
    data1  
    ```  
  
7.  将文本框的 DataField 属性更改为以下：  
  
    ```  
    customer_id  
    ```  
  
8.  运行该窗体，并使用数据控件从 Visual FoxPro TasTrade 示例数据库的客户 id 字段通过跳过。
