---
title: XML 安全注意事项 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e80a0bbb70a626ff01043592896ecfbe3c21f189
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47802876"
---
# <a name="xml-security-considerations"></a>XML 安全注意事项
ADO 保存和打开记录集对象上的方法不考虑安全操作，在 Internet Explorer 中运行。 因此，如果正在运行的应用程序或浏览器承载的控件中的脚本代码中使用这些方法，在浏览器的安全配置将会影响其行为。  
  
 Internet Explorer 5 默认情况下，在 Internet 区域中提供此类操作的安全限制。 在该配置下，记录集不能对客户端上的本地文件系统进行任何访问权限或访问的服务器从其下载页面的域之外的任何数据源。 具体而言，当浏览器主机内运行，记录集可以保存保存到文件仅当在同一台服务器从其下载页面。 同样，仅当该文件是在同一台服务器从其下载页面从文件加载来打开记录集。  
  
## <a name="see-also"></a>请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
