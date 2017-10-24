---
title: "ALTER ENDPOINT (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER ENDPOINT
- ALTER_ENDPOINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ENDPOINT statement
- modifying endpoints
- endpoints [SQL Server], modifying
ms.assetid: 70f35566-30cf-47c6-8394-dfe5d71629d3
caps.latest.revision: 56
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2552e1b3ece67afb0f73b1ab9e1f9911ee235703
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-endpoint-transact-sql"></a>ALTER ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  允许通过以下方法修改现有端点：  
  
-   向现有端点中添加一个新方法。  
  
-   修改或删除端点中的现有方法。  
  
-   更改端点的属性。  
  
> [!NOTE]  
>  本主题描述了特定于 ALTER ENDPOINT 的语法和参数。 有关创建终结点和 ALTER ENDPOINT 均通用的自变量的说明，请参阅[CREATE ENDPOINT &#40;Transact SQL &#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，删除了本机 XML Web 服务（SOAP/HTTP 端点）  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
[ AS { TCP } ( <protocol_specific_items> ) ]  
[ FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_items>  
        ) ]  
  
<AS TCP_protocol_specific_arguments> ::=  
AS TCP (  
  LISTENER_PORT = listenerPort  
  [ [ , ] LISTENER_IP = ALL | ( 4-part-ip ) | ( "ip_address_v6" ) ]  
)  
<FOR SERVICE_BROKER_language_specific_arguments> ::=  
FOR SERVICE_BROKER (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
   ]  
  
  [ , MESSAGE_FORWARDING = {ENABLED | DISABLED} ]  
  [ , MESSAGE_FORWARD_SIZE = forwardSize  
)  
  
<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
  
```  
  
## <a name="arguments"></a>参数  
  
> [!NOTE]  
>  以下参数特定于 ALTER ENDPOINT。 其余的自变量的说明，请参阅[CREATE ENDPOINT &#40;Transact SQL &#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 **AS** { **TCP** }  
 无法更改使用的传输协议**ALTER ENDPOINT**。  
  
 **授权***登录名*  
 **授权**选项将不可用在**ALTER ENDPOINT**。 只能在创建端点时分配所有权。  
  
 **有关**{ **TSQL** | **SERVICE_BROKER** | **DATABASE_MIRRORING** }  
 无法更改具有的负载类型**ALTER ENDPOINT**。  
  
## <a name="remarks"></a>注释  
 在使用 ALTER ENDPOINT 时，请仅指定要更新的参数。 除非进行显式更改，否则现有端点的所有属性均保持不变。  
  
 不能在用户事务中执行 ENDPOINT DDL 语句。  
  
 有关选择加密算法用于与终结点的信息，请参阅[选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)。  
  
> [!NOTE]  
>  RC4 算法仅用于支持向后兼容性。 仅当数据库兼容级别为 90 或 100 时，才能使用 RC4 或 RC4_128 对新材料进行加密。 （建议不要使用。）而是使用一种较新的算法，如 AES 算法之一。 在[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更高版本，使用 RC4 或 RC4_128 加密的材料可以进行解密在任何兼容级别。  
>   
>  RC4 是一个相对较弱的算法，而 AES 是一个相对较强的算法。 但是 AES 比 RC4 慢得多。 如果安全性的优先级高于速度，则建议使用 AES。  
  
## <a name="permissions"></a>Permissions  
 用户必须是属于**sysadmin**固定服务器角色，该终结点的所有者或已被授予 ALTER ANY ENDPOINT 权限。  
  
 若要更改现有端点的所有权，必须使用 ALTER AUTHORIZATION 语句。 有关详细信息，请参阅[ALTER AUTHORIZATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 有关详细信息，请参阅 [GRANT 终结点权限 (Transact-SQL)](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [DROP ENDPOINT (Transact SQL)](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

