---
title: srv_describe（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_describe
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_describe
ms.assetid: 2115600e-5ce7-4be0-9cd3-a1dd1fab0729
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 64910ce8bab155639a16cb065768c43fd86ac737
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127334"
---
# <a name="srvdescribe-extended-stored-procedure-api"></a>srv_describe（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 定义行中特定列的列名以及源数据类型和目标数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_describe (  
SRV_PROC *  
srvproc  
,  
int  
colnumber  
,  
DBCHAR *  
column_name  
,  
int  
namelen  
,  
DBINT  
desttype  
,  
DBINT  
destlen  
,  
DBINT  
srctype  
,  
DBINT  
srclen  
,  
void *  
srcdata  
);  
  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接（在本例中为发送相应行的客户端）句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的所有信息。  
  
 colnumber  
 当前不受支持。 必须按顺序描述列。 必须在调用 srv_sendrow 之前对所有列进行描述。  
  
 column_name  
 指定数据所属列的名称。 该参数可以为 NULL，因为列不是必须要有名称。  
  
 namelen  
 指定 column_name 的长度（以字节为单位）。 如果 namelen 为 SRV_NULLTERM，则 column_name 必须以 Null 值终止。  
  
 desttype  
 指定目标行列的数据类型。 这是发送到客户端的数据类型。 即使数据为 NULL，也必须指定数据类型。有关详细信息，请参阅[数据类型（扩展存储过程 API）](data-types-extended-stored-procedure-api.md)。  
  
 destlen  
 指定要发送到客户端的数据的长度（单位为字节）。 对于不允许使用 Null 值的固定长度的数据类型，将忽略 destlen。 对于可变长度的数据类型和允许使用 Null 值的固定长度的数据类型，destlen 指定目标数据可以达到的最大长度。  
  
 srctype  
 指定源数据的数据类型。  
  
 srclen  
 指定源数据的长度（单位为字节）。 对于固定长度数据类型，则忽略该值。  
  
 srcdata  
 提供特定列的源数据地址。 调用 srv_sendrow 时，它将在 srcdata 处查找 colnumber 的数据。 因此，在调用 srv_sendrow 前不应释放它。 可以通过使用 srv_setcoldata 在 srv_sendrow 的调用之间更改源数据地址。 在将列数据替换为对 srv_setcoldata 的其他调用或调用 srv_senddone 之前，不应释放为 srcdata 分配的内存。  
  
 如果 desttype 为 SRVDECIMAL 或 SRVNUMERIC，则 srcdata 参数必须为指向 DBNUMERIC 或 DBDECIMAL 结构的指针，并且此结构的精度和小数位数字段必须已设置为所需的值。 您可以使用 DEFAULTPRECISION 指定一个默认精度，使用 DEFAULTSCALE 指定一个默认小数位数。  
  
## <a name="returns"></a>返回  
 所描述的列的编号。 第一列为列 1。 如果出现错误，则返回 0。  
  
## <a name="remarks"></a>备注  
 在首次调用 srv_sendrow 之前，必须为行中的每一列调用一次 srv_describe 函数。 可以按任意顺序描述行的各列。  
  
 若要在发送整个结果集之前更改列行中源数据的位置和长度，请分别使用 srv_setcoldata 和 srv_setcollen。  
  
 有关数据类型和扩展存储过程 API 数据类型转换的说明，请参阅[数据类型（扩展存储过程 API）](data-types-extended-stored-procedure-api.md)。  
  
 如果应用程序中的列名为 Unicode 格式，则在调用 srv_describe 前需要将该列名转换为服务器的多字节代码页。 有关详细信息，请参阅 [Unicode 数据和服务器代码页](../extended-stored-procedures-programming/unicode-data-and-server-code-pages.md)。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>请参阅  
 [srv_sendrow（扩展存储过程 API）](srv-sendrow-extended-stored-procedure-api.md)   
 [srv_setutype（扩展存储过程 API）](srv-setutype-extended-stored-procedure-api.md)   
 [srv_setcoldata（扩展存储过程 API）](srv-setcoldata-extended-stored-procedure-api.md)  
  
  
