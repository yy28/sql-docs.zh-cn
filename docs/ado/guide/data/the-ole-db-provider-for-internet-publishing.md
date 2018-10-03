---
title: 用于 Internet 发布的 OLE DB 访问接口 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f70970ec872d3c921fa10e3eacb1c54d7c4de2d4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632205"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>用于 Internet 发布的 OLE DB 提供程序
ADO[记录](../../../ado/reference/ado-api/record-object-ado.md)并[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象可以在 Microsoft OLE DB 访问接口为 Internet 发布 （Internet 发布提供程序） 访问和处理资源，例如 Web 文件夹或文件由 Microsoft FrontPage 提供服务。 使用 ADO 中，您可以指定的源**记录**， **Stream**，或[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)是 url。 你可以然后上传、 下载、 移动、 复制和删除资源，或直接操作资源属性。  
  
 例如使用的代码**记录**并**流**与 Internet 发布提供程序，请参阅[Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)。  
  
 Internet 发布提供程序随 Microsoft Windows 2000。 早期版本的 Internet 发布提供程序还将提供 Microsoft Office 2000 和 Microsoft Internet Explorer 5.0。  
  
 有三种方法来将 ADO 连接到 Internet 发布提供程序：  
  
-   指定"URL ="连接字符串中。 例如：  
  
    ```  
    objConn.Open "URL=http://servername"  
    ```  
  
-   指定为 Msdaipp.dso*提供程序*的连接字符串关键字。 例如：  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=http://servername"  
    ```  
  
-   指定为 Msdaipp.dso[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)的属性[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。 例如：  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "http://servername"  
    ```  
  
> [!NOTE]
>  如果提供程序，使用的值作为显式指定 Msdaipp.dso*提供程序*连接字符串关键字或**提供程序**属性，不能使用"URL ="连接字符串中。 如果这样做，将会出错。 如前面所示，只需指定的 URL。  
  
 有关 Internet 发布提供程序的更多具体信息，请参阅[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，或提供与其源应用程序的提供程序文档的 OLE DB 访问接口安装了 Internet 发布： Windows 2000、 Office 2000 或 Internet Explorer 5.0。
