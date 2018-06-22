---
title: 警报属性： 新警报 （选项页） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b5e65400a2b7f82316ecdae3f92d34e40ac0715e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017015"
---
# <a name="alert-properties-new-alert-options-page"></a>警报属性： 新警报 （选项页）
  使用此页可以查看和修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报的选项。  
  
## <a name="options"></a>“常规”  
 **电子邮件**  
 在电子邮件通知中包括事件错误文本（如果有的话）。  
  
 **寻呼程序**  
 在寻呼程序通知中包括事件错误文本（如果有的话）。  
  
 **Net send**  
 在 net send 通知中包括事件错误文本（如果有的话）。  
  
 **要发送的其他通知消息**  
 键入要包括在通知消息中的任何其他文本。  
  
 **两次响应之间的延迟时间**  
 为重复发生的事件指定延迟时间。 某些事件可能会在短期内频繁发生。 在这种情况下，您可能需要知道事件已经发生，但不希望针对每一事件做出响应。 使用此选项可以指定超时时间。如果设定了延迟时间，在警报响应某个事件之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将等待指定的延迟时间，然后再响应，而不管在延迟时间内该事件发生与否。  
  
 **Minutes**  
 指定延迟时间（分钟）。 若要在每次发生事件时均予以响应，请指定 0 分和 0 秒。  
  
 **Seconds**  
 指定延迟时间（秒）。 若要在每次发生事件时均予以响应，请指定 0 分和 0 秒。  
  
## <a name="see-also"></a>请参阅  
 [警报](alerts.md)  
  
  