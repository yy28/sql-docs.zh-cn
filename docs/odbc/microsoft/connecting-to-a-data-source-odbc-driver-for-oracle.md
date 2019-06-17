---
title: 连接到数据源 （Oracle ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: adee8d8dd8d6db0d79b37ff853c41e7604fe21de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63302133"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>连接到数据源（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 ODBC 应用程序可以通过多种方式传递的连接信息。 例如，应用程序可能具有驱动程序始终提示用户输入连接信息。 或应用程序可能希望指定数据源连接的连接字符串。 如何连接到数据源取决于 ODBC 应用程序所使用的连接方法。  
  
 一种常用的方式连接到数据源是通过数据源对话框。 如果 ODBC 应用程序设置为使用一个对话框，该对话框会显示，并将提示您输入适当的数据源连接信息。  
  
 此外可以连接到数据源使用[连接字符串](../../odbc/microsoft/connection-string-format-and-attributes.md)。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>若要连接到使用对话框中的数据源  
  
1.  数据源对话框出现时，选择 Oracle 数据源，然后单击确定。 连接对话框。  
  
2.  填写连接对话框中的相应信息，然后单击确定。  
  
 连接后对信息进行验证，你的应用程序可以使用用于 Oracle 的 ODBC 驱动程序来访问数据源包含的信息。
