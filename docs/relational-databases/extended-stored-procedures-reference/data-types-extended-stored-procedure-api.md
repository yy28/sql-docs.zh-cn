---
title: 数据类型（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0e703c80db732560a45db72d8f8c0bf2a2ce21fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="data-types-extended-stored-procedure-api"></a>数据类型（扩展存储过程 API）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 若要使用扩展存储过程 API 数据类型，请在程序中包括 Srv.h 头文件。  
  
|数据类型|SQL Server 数据类型|Description|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|**binary**|binary 数据类型，长度为 0 至 8000 个字节。|  
|SRVBIGCHAR|**char**|character 数据类型，长度为 0 至 8000 个字节。|  
|SRVBIGVARBINARY|**varbinary**|长度可变的 binary 数据类型，长度为 0 至 8000 个字节。|  
|SRVBIGVARCHAR|**varchar**|长度可变的 character 数据类型，长度为 0 至 8000 个字节。|  
|SRVBINARY|**binary**|binary 数据类型。|  
|SRVBIT|**Bit**|bit 数据类型。|  
|SRVBITN|**bit null**|bit 数据类型，允许为 null 值。|  
|SRVCHAR|**char**|character 数据类型。|  
|SRVDATETIME|**datetime**|8 字节的 datetime 数据类型。|  
|SRVDATETIM4|**smalldatetime**|4 字节的 smalldatetime 数据类型。|  
|SRVDATETIMN|**datetime null**|smalldatetime 或 datetime 数据类型，允许为 null 值。|  
|SRVDECIMAL|**decimal**|decimal 数据类型。|  
|SRVDECIMALN|**decimal null**|decimal 数据类型，允许为 null 值。|  
|SRVFLT4|**real**|4 字节的 real 数据类型。|  
|SRVFLT8|**float**|8 字节的 float 数据类型。|  
|SRVFLTN|**real** &#124; **float null**|real 或 float 数据类型，允许为 null 值。|  
|SRVIMAGE|**图像**|image 数据类型。|  
|SRVINT1|**tinyint**|1 字节的 tinyint 数据类型。|  
|SRVINT2|**int**|2 字节的 smallint 数据类型。|  
|SRVINT4|**int**|4 字节的 int 数据类型。|  
|SRVINTN|**tinyint** &#124; **smallint** &#124; **int null**|tinyint、smallint 或 int 数据类型，允许为 null 值。|  
|SRVMONEY4|**smallmoney**|4 字节的 smallmoney 数据类型。|  
|SRVMONEY|**money**|8 字节的 money 数据类型。|  
|SRVMONEYN|**money** &#124; **smallmoney null**|smallmoney 或 money 数据类型，允许为 null 值。|  
|SRVNCHAR|**nchar**|Unicode character 数据类型。|  
|SRVNTEXT|**ntext**|Unicode text 数据类型。|  
|SRVNUMERIC|**numeric**|numeric 数据类型。|  
|SRVNUMERICN|**numeric null**|numeric 数据类型，允许为 null 值。|  
|SRVNVARCHAR|**nvarchar**|Unicode 长度可变的 character 数据类型。|  
|SRVTEXT|**text**|text 数据类型。|  
|SRVVARBINARY|**varbinary**|长度可变的 binary 数据类型。|  
|SRVVARCHAR|**varchar**|长度可变的 character 数据类型。|  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
  
