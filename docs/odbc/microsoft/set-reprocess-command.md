---
title: SET 重新处理命令 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb1ee7ee957ef5a7872a87a47d5615f1d241aa6b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="set-reprocess-command"></a>SET 重新处理命令
指定多少时间或如何长度后不成功的锁定尝试锁定文件或记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>参数  
 到*nAttempts*[SECONDS]  
 指定的次数或尝试后失败的初始尝试锁定记录或文件的秒数。 默认值为 0;最大值为 32000。  
  
 秒指定 Visual FoxPro 尝试锁定某个文件，或记录*nAttempts*秒。 它是时才可用*nAttempts*大于零。  
  
 例如，如果*nAttempts*为 30，Visual FoxPro 尝试锁定记录或文件最多 30 次。 如果你还包括秒 （设置重新处理到 30 秒为单位），Visual FoxPro 持续尝试最多 30 秒锁定记录或文件。  
  
 如果 ON 错误例程有效并且锁定记录或文件的命令的尝试均不成功，将执行 ON 错误例程。 但是，如果函数尝试锁定，ON 错误例程不执行，此函数返回 False (。F.) 中。  
  
 如果 ON 错误例程也不会生效，命令将尝试锁定记录或文件，也不能放置锁，会生成错误。 如果函数尝试将放置锁，不显示警报，并且此函数返回 False (。F.) 中。  
  
 如果*nAttempts*为 0 （默认值） 和发出的命令或尝试锁定记录或文件的函数，则 Visual FoxPro 尝试锁定记录或无限期地文件。 如果记录或文件变得可用于锁定等待时，放置锁，并清除系统消息。 如果函数尝试将放置锁，函数将返回 True (。T。) 中。  
  
 如果 ON 错误例程生效，并且命令尝试锁定记录或文件，ON 错误例程优先于锁定记录或文件的更多尝试。 ON 错误例程将立即执行。 Visual FoxPro 不会尝试其他记录或文件锁定，并且不显示系统消息。  
  
 如果*nAttempts*为 1、 Visual FoxPro 尝试锁定记录或无限期地文件和 ON 错误例程不执行。  
  
 如果已由另一个用户在记录或都尝试锁定的文件上放置锁，你必须等待，直到用户释放的锁。  
  
 为自动  
 指定 Visual FoxPro 尝试锁定记录或无限期地文件。 （为-2 的集重新处理是等效的命令。）  
  
## <a name="remarks"></a>注释  
 第一次尝试锁定记录或文件并不总是成功。 通常情况下，记录或文件已由网络上的另一个用户锁定。 设置重新处理确定 Visual FoxPro 是否使最初尝试不成功时锁定记录或文件的更多尝试。 你可以指定多少次的更多尝试进行，或对于多长时间尝试将生成。 ON 错误例程会影响如何不成功尝试处理的锁。
