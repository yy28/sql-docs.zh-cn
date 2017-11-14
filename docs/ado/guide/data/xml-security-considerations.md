---
title: "XML 安全注意事项 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fc94f80cde09f6ad55de3a108b6fd16ef74444f1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="xml-security-considerations"></a>XML 安全注意事项
ADO 保存和打开记录集对象上的方法不考虑安全操作，以在 Internet Explorer 中运行。 因此，如果这些方法将用在应用程序或浏览器中托管的控件中运行的脚本代码中，浏览器的安全配置会影响其行为。  
  
 Internet Explorer 5 默认情况下，Internet 区域中提供此类操作的安全限制。 在该配置下，记录集不能对客户端上的本地文件系统进行任何访问权限，或者访问从中下载页的服务器的域以外的任何数据源。 具体而言，运行时在浏览器主机内，记录集可以保存回文件仅是否在下载页面的同一服务器上。 同样，你可以通过仅当该文件在同一台服务器从其下载页从文件加载打开记录集。  
  
## <a name="see-also"></a>另请参阅  
 [保留记录采用 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)

