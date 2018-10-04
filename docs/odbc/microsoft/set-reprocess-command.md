---
title: SET REPROCESS 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41877986d5d0e8afdfb30841860df360efd26da0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649679"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 命令
指定多少时间或如何很长时间才能锁定尝试失败后将其锁定的文件或记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>参数  
 向*nAttempts*[秒]  
 指定的次数或尝试不成功初始尝试后锁定的记录或文件的秒数。 默认值为 0;最大值为 32,000。  
  
 秒指定 Visual FoxPro 尝试锁定的文件或记录*nAttempts*秒。 它是时才可用*nAttempts*大于零。  
  
 例如，如果*nAttempts*为 30，Visual FoxPro 尝试锁定记录或文件最多 30 次。 如果还包括秒 （设置重新处理到 30 秒），Visual FoxPro 持续尝试锁定的记录或文件，以最多 30 秒。  
  
 如果 ON ERROR 例程是否生效，并且如果某一命令锁定的记录或文件的尝试均不成功，则执行 ON ERROR 例程。 但是，如果函数尝试锁定，ON ERROR 例程不会执行，该函数将返回 False (。F.) 中。  
  
 如果 ON ERROR 例程也不会生效，命令将尝试锁定的记录或文件，并且不能放置锁，会生成错误。 如果函数尝试将放置锁，警报不显示，并且该函数将返回 False (。F.) 中。  
  
 如果*nAttempts*为 0 （默认值） 和发出的命令或尝试锁定的记录或文件的函数，则 Visual FoxPro 尝试锁定的记录或无限期文件。 如果记录或文件变得可用于锁定在等待时，放置锁，并清除系统消息。 如果函数尝试将放置锁，则函数返回 True (。T。)。  
  
 如果 ON ERROR 例程生效，并且命令尝试锁定的记录或文件，ON ERROR 例程优先于锁定的记录或文件的更多尝试。 ON ERROR 例程将立即执行。 Visual FoxPro 不会尝试其他记录或文件锁，不会显示系统消息。  
  
 如果*nAttempts*为 1、 Visual FoxPro 尝试锁定的记录或无限期文件和 ON ERROR 例程不会执行。  
  
 如果已由另一个用户都尝试锁定的文件的记录上放置锁，必须等待，直到用户释放锁。  
  
 为自动  
 指定 Visual FoxPro 尝试锁定的记录或无限期文件。 （-2 到集重新处理是等效的命令。）  
  
## <a name="remarks"></a>备注  
 第一次尝试锁定记录或文件并不总是成功。 通常情况下，记录或文件已由网络上的其他用户锁定。 设置重新处理确定 Visual FoxPro 是否使初始尝试不成功时锁定的记录或文件的更多尝试。 您可以指定更多的尝试都是或进行多长时间尝试的次数。 ON ERROR 例程会影响如何不成功的锁定尝试进行处理。
