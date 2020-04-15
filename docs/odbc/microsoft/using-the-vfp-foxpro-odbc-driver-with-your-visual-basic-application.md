---
title: 将 VFP FoxPro ODBC 驱动程序与您的视觉基本应用程序一起使用 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 871c392166fa2f5726e6f9e8651bf758dc144a00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292697"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>配合使用 VFP FoxPro ODBC 驱动程序和 Visual Basic 应用程序
您的 Microsoft®可视化基础®应用程序可以通过创建连接到 Visual FoxPro 数据源的数据控件与 Visual FoxPro 数据进行通信。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>使用可视化基础中的数据控制连接到 Visual FoxPro 数据  
  
1.  创建名为"测试"的数据源，该数据源连接到 Visual FoxPro 中包含的 TasTrade 示例数据库。 默认的 Visual FoxPro 安装将 TasTrade 示例数据库放在该位置：  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  在"视觉基本"中，创建新窗体，并在其中放置一个文本框和数据控件。  
  
3.  更改"数据"控件的 Connect 属性，如下所示：  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  将记录集类型属性更改为以下内容：  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  将 RecordSource 属性更改为以下内容：  
  
    ```  
    customer  
    ```  
  
6.  将文本框的 DataSource 属性更改为"数据"控件的默认名称，更改为以下内容：  
  
    ```  
    data1  
    ```  
  
7.  将文本框的 DataField 属性更改为以下内容：  
  
    ```  
    customer_id  
    ```  
  
8.  运行窗体，并使用数据控件跳过 Visual FoxPro TasTrade 示例数据库中的客户 ID 字段。
