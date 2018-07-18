---
title: sp_setapprole (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ac733afa3f8afef74a9d6affb16e0f9dbcd5b4a9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259054"
---
# <a name="spsetapprole-transact-sql"></a>sp_setapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  激活与当前数据库中的应用程序角色关联的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }   
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@rolename =** ] *****角色*****  
 当前数据库中定义的应用程序角色的名称。 *角色*是**sysname**，无默认值。 *角色*必须存在于当前数据库。  
  
 [  **@password =** ] **{加密 N***密码***}**  
 激活应用程序角色所需的密码。 *密码*是**sysname**，无默认值。 *密码*可以通过使用 ODBC 进行模糊处理**加密**函数。 当你使用**加密**函数，密码必须通过将转换为 Unicode 字符串**N**第一个引号前。  
  
 正在使用连接不支持加密选项**SqlClient**。  
  
> [!IMPORTANT]  
>  ODBC**加密**函数不提供加密。 您不应当依赖该函数来保护通过网络传输的密码。 如果通过网络传输该信息，则使用 SSL 或者 IPSec。  
  
 **@encrypt = 'none'**  
 指定不使用任何模糊代码。 密码以明文形式传递到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这是默认设置。  
  
 **@encrypt= odbc**  
 指定 ODBC 将模糊密码处理通过使用 ODBC**加密**发送到的密码前的函数[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 这只能在使用 ODBC 客户端或 OLE DB Provider for SQL Server 时指定。  
  
 [  **@fCreateCookie =** ] **true** | **false**  
 指定是否创建 cookie。 **true**隐式转换为 1。 **false**隐式转换为 0。  
  
 [  **@cookie =** ]  **@cookie输出**  
 指定包含 cookie 的输出参数。 仅当生成该 cookie 的值**@fCreateCookie**是**true**。 **varbinary(8000)**  
  
> [!NOTE]  
>  **sp_setapprole** 的 cookie **OUTPUT** 参数现记载为 **varbinary(8000)** ，这是正确的最大长度。 但是，目前执行返回 **varbinary(50)**。 应用程序应继续保留**varbinary （8000)** ，以便应用程序将继续正常运行，如果 cookie 返回大小增加的未来版本中。  
  
## <a name="return-code-values"></a>返回代码值  
 0 （成功） 和 1 （失败）  
  
## <a name="remarks"></a>注释  
 在应用程序后角色激活通过**sp_setapprole**，直到用户从服务器断开连接或执行的角色将保持活动**sp_unsetapprole**。 **sp_setapprole**可以仅通过直接执行[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。 **sp_setapprole**无法在其他存储过程中或在用户定义的事务中执行。  
  
 应用程序角色的概述，请参阅[应用程序角色](../../relational-databases/security/authentication-access/application-roles.md)。  
  
> [!IMPORTANT]  
>  为了在通过网络传输应用程序角色密码时对其进行保护，在启用应用程序角色时应始终使用加密连接。  
>   
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC**加密**选项不受**SqlClient**。 如果必须存储凭据，请使用加密 API 函数对这些凭据进行加密。 参数*密码*存储为单向哈希。 若要保留与早期版本的兼容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不强制密码复杂性策略**sp_addapprole**。 若要强制实施密码复杂性策略，请使用[CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**公共**和角色的密码的知识。  
  
## <a name="examples"></a>示例  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>A. 激活应用程序角色但不使用加密选项  
 以下示例使用明文密码 `SalesAppRole` 激活名为 `AsDeF00MbXX` 的应用程序角色，该密码是使用特别为当前用户使用的应用程序设计的权限创建的。  
  
```  
EXEC sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO  
```  
  
### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>B. 使用 cookie 激活应用程序角色并恢复到原始上下文中  
 以下示例使用密码 `Sales11` 激活 `fdsd896#gfdbfdkjgh700mM` 应用程序角色并创建一个 cookie。 该示例返回当前用户的名称，然后通过执行 `sp_unsetapprole` 恢复到原始上下文中。  
  
```  
DECLARE @cookie varbinary(8000);  
EXEC sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.   
GO   
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE (Transact-SQL)](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE (Transact-SQL)](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [sp_unsetapprole &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)  
  
  
