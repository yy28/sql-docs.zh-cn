---
title: Detail 属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
caps.latest.revision: 32
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: fa7a39ee74bcdd9399c6e06eff9ee6df4688653a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016754"
---
# <a name="detail-property"></a>Detail 属性
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]“SoapException”类的“Detail”属性具有以下 XML 结构：  
  
## <a name="elements"></a>元素  
 Detail  
 包含所有其他错误详细信息元素的顶级元素。  
  
 **ErrorCode**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 特定的错误代码。  
  
 HttpStatus  
 HTTP 状态代码。  
  
 **Message**  
 报表服务器分配的错误消息和错误代码。  
  
 HelpLink  
 指向某网站的帮助链接 URL，在该网站中可以找到有关错误的更多信息。 有关详细信息，请参阅 [HelpLink 元素](helplink-element.md)。  
  
 LinkID  
 分配给链接的 ID。  
  
 ProductName  
 产品的名称。 默认值为“Microsoft SQL Server Reporting Services”。  
  
 ProductVersion  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的版本。 最大长度为 15 个字符。 版本号的格式应如下所示：8.00.0xxx.00。  
  
 ProductLocaleId  
 应用程序的 INTL DLL 的区域设置 ID 或语言 ID（例如，0x41A）。  
  
 OperatingSystem  
 在其中安装 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的操作系统。 有效值包括：“0”表示独立于操作系统，“1”表示 [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)]，“16”表示 Windows XP。  
  
 CountryLocaleId  
 操作系统的区域设置 ID 或语言 ID。 例如，对应于 Windows 法语版的值为 0x040c。  
  
 MoreInformation  
 一个 XML 字符串，其中包含在运行方法时出现的嵌套异常。  
  
 **数据源**  
 “MoreInformation”的一个子元素。 错误的源。  
  
 **Message**  
 “MoreInformation”的一个子元素。 嵌套异常的错误消息。 此元素包含“ErrorCode”和“HelpLink”的 XML 属性。  
  
 **警告**  
 一个 XML 字符串，其中包含从报表处理返回的警告。  
  
## <a name="see-also"></a>请参阅  
 [介绍 Reporting Services 中的异常处理](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](reporting-services-soapexception-class.md)   
 [使用 Detail 属性处理特定错误](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  