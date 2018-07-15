---
title: srv_convert（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_convert
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_convert
ms.assetid: 216b4a31-786e-4361-8a33-e5f6e9790f90
caps.latest.revision: 33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6b3324bfef3d9c00cd32d6616971127c5ef80c03
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285223"
---
# <a name="srvconvert-extended-stored-procedure-api"></a>srv_convert（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 将数据从一个数据类型更改为另一数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_convert (  
SRV_PROC *  
srvproc  
,  
int  
srctype  
,  
void *  
src  
,  
DBINT  
srclen  
,  
int  
desttype  
,  
void *  
dest  
,  
DBINT  
destlen  
);  
  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 用于管理应用程序和客户端之间的通信和数据的所有控制信息。 如果提供了 srvproc 句柄，在发生错误时它则会被传递给扩展存储过程 API 错误处理程序函数。  
  
 srctype  
 指定要转换的数据的数据类型。 该参数可以为任意一种扩展存储过程 API 数据类型。  
  
 *src*  
 指向要转换的数据的指针。 该参数可以为任意一种扩展存储过程 API 数据类型。  
  
 srclen  
 指定要转换的数据的长度（单位为字节）。 如果 srclen 为 0，srv_convert 将向目标变量中放入一个 Null 值。 除非它为 0，否则对于固定长度数据类型，会忽略该参数，在这种情况下会假定源数据为 NULL。 对于 SRVCHAR 数据类型的数据，长度为 -1 表示字符串以 Null 值结束。  
  
 desttype  
 指示要将源转换为何种数据类型。 该参数可以为任意一种扩展存储过程 API 数据类型。  
  
 dest  
 指向接收转换后的数据的目标变量的指针。 如果该指针为 NULL，srv_convert 将调用用户提供的错误处理程序（如果有的话），并返回 -1。  
  
 如果 desttype 为 SRVDECIMAL 或 SRVNUMERIC，则 dest 参数必须为指向 DBNUMERIC 或 DBDECIMAL 结构的指针，并且此结构的精度和小数位数字段必须已设置为所需的值。 您可以使用 DEFAULTPRECISION 指定一个默认精度，使用 DEFAULTSCALE 指定一个默认小数位数。  
  
 destlen  
 指定目标变量的长度（单位为字节）。 对于固定长度数据类型，则会忽略该参数。 对于 SRVCHAR 类型的目标变量，destlen 的值必须为目标缓冲区空间的总长度。 SRVCHAR 或 SRVBINARY 类型的目标变量的长度为 -1 时，表示有足够的可用空间。 对于 srvchar 类型的目标变量，长度为 -1 将使字符串以 Null 值终止。  
  
## <a name="returns"></a>返回  
 如果数据类型转换成功，则返回转换后的数据的长度（单位为字节）。 当 srv_convert 遇到它不支持的转换请求时，它将调用开发人员提供的错误处理程序（如果有），设置全局错误号，并返回 -1。  
  
## <a name="remarks"></a>Remarks  
 srv_willconvert 函数决定是否允许进行特定转换。  
  
 转换为近似的数字数据类型 SRVFLT4 或 SRVFLT8 可能会造成一定的精度损失。 从近似的数字数据类型 SRVFLT4 或 SRVFLT8 转换为 SRVCHAR 或 SRVTEXT 也可能造成一定的精度损失。  
  
 转换为 SRVFLT*x*、SRVINT*x*、SRVMONEY、SRVMONEY4、SRVDECIMAL 或 SRVNUMERIC 时，如果数字大于目标的最大值，则可能导致溢出，如果数字小于目标的最小值，则可能导致下溢。 如果在转换为 SRVCHAR 或 SRVTEXT 时发生上溢，则所得值的第一个字符将包含一个星号 (*)，以指示出错。  
  
 将 SRVCHAR 转换为 SRVBINARY 时，srv_convert 将 SRVCHAR 解释为十六进制，无论字符串是否包含前导 0 都是如此。 将 SRVBINARY 转换为 SRVCHAR 时，srv_convert 将创建一个不带前导 0 的十六进制字符串。 在所有其他情况下，以 SRVBINARY 数据类型为目标类型或源类型的转换都是直接逐位复制。  
  
 在某些情况下，将数据类型转换为自身可能比较有用。 例如，将 SRVCHAR 转换为 destlen 为 -1 的 SRVCHAR 将向字符串添加一个 Null 终止符。  
  
 有关数据类型和扩展存储过程 API 数据类型转换的说明，请参阅[数据类型（扩展存储过程 API）](data-types-extended-stored-procedure-api.md)。  
  
 srv_convert 函数可能会因以下几种原因失败：  
  
-   请求的转换不可用。  
  
-   转换导致目标变量出现截断、上溢或精度损失。  
  
-   将字符串转换为数字数据类型时出现语法错误。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>请参阅  
 [srv_setutype（扩展存储过程 API）](srv-setutype-extended-stored-procedure-api.md)   
 [srv_willconvert（扩展存储过程 API）](srv-willconvert-extended-stored-procedure-api.md)  
  
  
