---
title: "OLE DB Provider for Internet 发布 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5731b15274e4d2c1acafec09bd6478fc244a1f59
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>OLE DB Provider for Internet 发布
ADO[记录](../../../ado/reference/ado-api/record-object-ado.md)和[流](../../../ado/reference/ado-api/stream-object-ado.md)对象可以用于使用 Microsoft OLE DB 提供程序 Internet 发布 （Internet 发布提供程序） 访问和处理资源，如 Web 文件夹或文件由 Microsoft FrontPage 提供服务。 使用 ADO，您可以指定的源**记录**，**流**，或[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)是 url。 你可以然后上载、 下载、 移动、 复制和删除资源，或直接操作资源属性。  
  
 有关代码示例使用**记录**和**流**与 Internet 发布提供程序，请参阅[Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)。  
  
 Internet 发布提供程序安装 Microsoft Windows 2000。 早期版本的 Internet 发布提供程序还将提供 Microsoft Office 2000 和 Microsoft Internet Explorer 5.0。  
  
 有三种方法来将 ADO 连接到 Internet 发布提供程序：  
  
-   指定"URL ="连接字符串中。 例如：  
  
    ```  
    objConn.Open "URL=http://servername"  
    ```  
  
-   指定有关 Msdaipp.dso*提供程序*的连接字符串关键字。 例如：  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=http://servername"  
    ```  
  
-   指定有关 Msdaipp.dso[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 例如：  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "http://servername"  
    ```  
  
> [!NOTE]
>  如果 Msdaipp.dso 显式指定的提供程序，使用值为*提供程序*连接字符串关键字或**提供程序**属性，不能使用"URL ="连接字符串中。 如果这样做，将会出错。 如前面所示相反，只需指定的 URL。  
  
 有关 Internet 发布提供程序的详细信息，请参阅[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，或与与其源应用程序提供的提供程序文档 OLE DB Provider forInternet 发布已安装： Windows 2000、 Office 2000 或 Internet Explorer 5.0。
