---
title: 连接到数据源 （适用于 Oracle 的 ODBC 驱动程序） |Microsoft 文档
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
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c12472544fd843214cab4294311889d0a84010d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>连接到数据源 （适用于 Oracle 的 ODBC 驱动程序）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 ODBC 应用程序可以通过多种方式传入连接信息。 例如，应用程序可能具有始终提示用户输入连接信息的驱动程序。 或应用程序可能会收到一个连接字符串，指定数据源连接。 如何连接到数据源取决于 ODBC 应用程序使用的连接方法。  
  
 一种常用方式连接到数据源是通过数据源对话框。 如果 ODBC 应用程序设置为使用对话框中，该对话框将显示，并将提示你输入适当的数据源连接信息。  
  
 你还可以连接到数据源使用[连接字符串](../../odbc/microsoft/connection-string-format-and-attributes.md)。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>若要连接到使用对话框中的数据源  
  
1.  当出现数据源对话框时，选择 Oracle 数据源，，然后单击确定。 连接对话框。  
  
2.  中的相应信息来连接对话框中，填写，然后单击确定。  
  
 连接后信息进行验证，你的应用程序可以使用用于 Oracle 的 ODBC 驱动程序来访问数据源包含的信息。
