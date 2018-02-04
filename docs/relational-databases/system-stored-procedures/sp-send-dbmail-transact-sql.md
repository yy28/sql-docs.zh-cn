---
title: sp_send_dbmail (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sendmail_sp_TSQL
- sendmail_sp
- SP_SEND_DBMAIL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_send_dbmail
ms.assetid: f1d7a795-a3fd-4043-ac4b-c781e76dab47
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7293e16e45c465fa2cfeda2d11888b4dc450d380
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="spsenddbmail-transact-sql"></a>sp_send_dbmail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向指定收件人发送电子邮件。 该邮件可能包含查询结果集和/或文件附件。 在邮件成功放置在数据库邮件队列时**sp_send_dbmail**返回**mailitem_id**的消息。 此存储的过程位于**msdb**数据库。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_send_dbmail [ [ @profile_name = ] 'profile_name' ]  
    [ , [ @recipients = ] 'recipients [ ; ...n ]' ]  
    [ , [ @copy_recipients = ] 'copy_recipient [ ; ...n ]' ]  
    [ , [ @blind_copy_recipients = ] 'blind_copy_recipient [ ; ...n ]' ]  
    [ , [ @from_address = ] 'from_address' ]  
    [ , [ @reply_to = ] 'reply_to' ]   
    [ , [ @subject = ] 'subject' ]   
    [ , [ @body = ] 'body' ]   
    [ , [ @body_format = ] 'body_format' ]  
    [ , [ @importance = ] 'importance' ]  
    [ , [ @sensitivity = ] 'sensitivity' ]  
    [ , [ @file_attachments = ] 'attachment [ ; ...n ]' ]  
    [ , [ @query = ] 'query' ]  
    [ , [ @execute_query_database = ] 'execute_query_database' ]  
    [ , [ @attach_query_result_as_file = ] attach_query_result_as_file ]  
    [ , [ @query_attachment_filename = ] query_attachment_filename ]  
    [ , [ @query_result_header = ] query_result_header ]  
    [ , [ @query_result_width = ] query_result_width ]  
    [ , [ @query_result_separator = ] 'query_result_separator' ]  
    [ , [ @exclude_query_output = ] exclude_query_output ]  
    [ , [ @append_query_error = ] append_query_error ]  
    [ , [ @query_no_truncate = ] query_no_truncate ]   
    [ , [ @query_result_no_padding = ] @query_result_no_padding ]   
    [ , [ @mailitem_id = ] mailitem_id ] [ OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@profile_name=** ] **'***profile_name***'**  
 发送邮件的配置文件的名称。 *Profile_name*属于类型**sysname**，默认值为 NULL。 *Profile_name*必须是现有数据库邮件配置文件的名称。 如果没有*profile_name*指定，则**sp_send_dbmail**为当前用户使用默认的专用配置文件。 如果用户不具有默认私有配置文件， **sp_send_dbmail**使用的默认公共配置文件**msdb**数据库。 如果用户没有默认的专用配置文件，并且没有数据库，没有默认公共配置文件 **@profile_name** 必须指定。  
  
 [ **@recipients=** ] **'***recipients***'**  
 要向其发送邮件的电子邮件地址列表，以分号分隔。 收件人列表属于类型**varchar （max)**。 虽然此参数是可选的但至少一个 **@recipients** ，  **@copy_recipients** ，或 **@blind_copy_recipients** 必须指定或**sp_send_dbmail**返回错误。  
  
 [ **@copy_recipients=** ] **'***copy_recipients***'**  
 要向其抄送邮件的电子邮件地址列表，以分号分隔。 复制收件人列表属于类型**varchar （max)**。 虽然此参数是可选的但至少一个 **@recipients** ，  **@copy_recipients** ，或 **@blind_copy_recipients** 必须指定或**sp_send_dbmail**返回错误。  
  
 [ **@blind_copy_recipients=** ] **'***blind_copy_recipients***'**  
 要向其密件抄送邮件的电子邮件地址列表，以分号分隔。 密件抄送收件人列表属于类型**varchar （max)**。 虽然此参数是可选的但至少一个 **@recipients** ，  **@copy_recipients** ，或 **@blind_copy_recipients** 必须指定或**sp_send_dbmail**返回错误。  
  
 [ **@from_address=** ] **'***from_address***'**  
 电子邮件的“from address”的值。 这是一个可选参数，用于覆盖邮件配置文件中的设置。 此参数属于类型**varchar （max)**。 SMTP 安全设置决定是否接受这些覆盖。 如果未指定参数，则默认值为 NULL。  
  
 [ **@reply_to=** ] **'***reply_to***'**  
 电子邮件的“reply to address”的值。 它只接受一个电子邮件地址作为有效值。 这是一个可选参数，用于覆盖邮件配置文件中的设置。 此参数属于类型**varchar （max)**。 SMTP 安全设置决定是否接受这些覆盖。 如果未指定参数，则默认值为 NULL。  
  
 [ **@subject=** ] **'***subject***'**  
 是电子邮件的主题。 主题属于类型**nvarchar （255)**。 如果未指定主题，则默认为“SQL Server 消息”。  
  
 [ **@body=** ] **'***body***'**  
 是电子邮件的正文。 消息正文的类型是**nvarchar (max)**，默认值为 NULL。  
  
 [ **@body_format=** ] **'***body_format***'**  
 邮件正文的格式。 该参数属于类型**varchar （20)**，默认值为 NULL。 如果已指定，则待发邮件的标头设置会指示邮件正文具有指定格式。 该参数可能包含下列值之一：  
  
-   TEXT  
  
-   HTML  
  
 默认为 TEXT。  
  
 [ **@importance=** ] **'***importance***'**  
 邮件的重要性。 该参数属于类型**varchar(6)**。 该参数可能包含下列值之一：  
  
-   Low  
  
-   Normal  
  
-   High  
  
 默认值为 Normal。  
  
 [ **@sensitivity=** ] **'***sensitivity***'**  
 邮件的敏感度。 该参数属于类型**varchar(12)**。 该参数可能包含下列值之一：  
  
-   Normal  
  
-   Personal  
  
-   Private  
  
-   Confidential  
  
 默认值为 Normal。  
  
 [ **@file_attachments=** ] **'***file_attachments***'**  
 电子邮件附件的文件名列表，以分号分隔。 必须使用绝对路径指定列表中的文件。 附件列表属于类型**nvarchar (max)**。 默认情况下，数据库邮件会将文件附件限制在每个文件 1 MB 大小。  
  
 [ **@query=** ] **'***query***'**  
 要执行的查询。 查询结果可以作为文件附加，或包含在电子邮件的正文中。 查询的类型是**nvarchar (max)**，并且可以包含任何有效[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。 请注意在单独的会话，因此本地变量中的脚本调用中执行查询**sp_send_dbmail**均不可用于查询。  
  
 [ **@execute_query_database=** ] **'***execute_query_database***'**  
 存储过程在其中运行查询的数据库上下文。 该参数属于类型**sysname**，默认值为当前数据库。 此参数才适用如果 **@query** 指定。  
  
 [ **@attach_query_result_as_file=** ] *attach_query_result_as_file*  
 指定查询结果集是否作为附件返回。 *attach_query_result_as_file*属于类型**位**，默认值为 0。  
  
 时的值为 0，查询结果中包含的电子邮件正文的内容后 **@body** 参数。 如果值为 1，结果将以附件形式返回。 此参数才适用如果 **@query** 指定。  
  
 [ **@query_attachment_filename=** ] *query_attachment_filename*  
 指定查询结果集附件使用的文件名。 *query_attachment_filename*属于类型**nvarchar （255)**，默认值为 NULL。 忽略此参数时*attach_query_result*为 0。 当*attach_query_result*为 1，此参数为 NULL，数据库邮件创建一个任意的文件名。  
  
 [ **@query_result_header=** ] *query_result_header*  
 指定查询结果是否包含列标题。 Query_result_header 值的类型是**位**。 如果该值为 1，则查询结果包含列标题。 如果该值为 0，则查询结果不包含列标题。 此参数默认为**1**。 此参数才适用如果 **@query** 指定。  
  
 [ **@query_result_width** = ] *query_result_width*  
 用于设置查询结果的格式的线条宽度（字符）。 *Query_result_width*属于类型**int**，默认值为 256。 提供的值必须介于 10 和 32767 之间。 此参数才适用如果 **@query** 指定。  
  
 [ **@query_result_separator=** ] **'***query_result_separator***'**  
 用于分隔查询输出中的列的字符。 该分隔符是类型的**char （1)**。 默认为“ ”（空格）。  
  
 [ **@exclude_query_output=** ] *exclude_query_output*  
 指定是否使用电子邮件返回查询执行的输出。 **exclude_query_output**位，默认值为 0。 此参数为 0 时，执行**sp_send_dbmail**存储的过程将显示在控制台上作为查询执行的结果返回的消息。 当此参数为 1，执行**sp_send_dbmail**存储的过程不会在查询执行消息中的任何打印控制台。  
  
 [ **@append_query_error=** ] *append_query_error*  
 指定是否将发送电子邮件，当从中指定的查询返回的错误时 **@query** 自变量。 **append_query_error**是**位**，默认值为 0。 如果此参数的值为 1，则数据库邮件会发送电子邮件，并在电子邮件的正文中包括查询错误消息。 此参数为 0 时，数据库邮件不发送电子邮件和**sp_send_dbmail**结尾返回代码 1，指示失败。  
  
 [ **@query_no_truncate=** ] *query_no_truncate*  
 指定是否执行查询中使用的选项，可避免截断的大型可变长度数据类型 (**varchar （max)**， **nvarchar (max)**， **varbinary （max)****xml**，**文本**， **ntext**，**映像**，和用户定义数据类型)。 设置该选项后，查询结果将不包含列标题。 *Query_no_truncate*值的类型是**位**。 当该值为 0 或未指定时，查询中的列将截断为 256 个字符。 当该值为 1 时，不截断查询中的列。 此参数的默认值为 0。  
  
> [!NOTE]  
>  在使用大量的数据，@**query_no_truncate**选项使用其他资源，并降低服务器的性能。  
  
 [ **@query_result_no_padding** ] *@query_result_no_padding*  
 类型为 bit。 默认值为 0。 如果设置为 1 时，查询结果将不填充，可能减小文件尺寸。如果你设置@query_result_no_padding设置为 1 和你@query_result_width参数，@query_result_no_padding参数将覆盖@query_result_width参数。  
  
 在这种情况下，不发生错误。  
  
 如果你设置@query_result_no_padding设置为 1 和你@query_no_truncate引发参数，出现错误。  
  
 [  **@mailitem_id=** ] *mailitem_id* [输出]  
 可选的输出参数返回*mailitem_id*的消息。 *Mailitem_id*属于类型**int**。  
  
## <a name="return-code-values"></a>返回代码值  
 返回代码 0 表示成功。 任何其他值表示失败。 失败的语句的错误代码存储在 @@ERROR变量。  
  
## <a name="result-sets"></a>结果集  
 成功时，返回消息“邮件已排队”。  
  
## <a name="remarks"></a>注释  
 开始使用前数据库邮件必须启用使用数据库邮件配置向导，或**sp_configure**。  
  
 **sysmail_stop_sp**停止数据库邮件通过停止外部程序使用的 Service Broker 对象。 **sp_send_dbmail**仍然接受邮件时数据库邮件已停止使用**sysmail_stop_sp**。 若要启动数据库邮件，使用**sysmail_start_sp**。  
  
 当 **@profile** 未指定， **sp_send_dbmail**使用默认配置文件。 如果发送电子邮件的用户具有默认专用配置文件，则数据库邮件使用该配置文件。 如果用户具有没有默认专用配置文件， **sp_send_dbmail**使用默认公共配置文件。 如果用户没有默认专用配置文件，且没有默认公共配置文件， **sp_send_dbmail**返回错误。  
  
 **sp_send_dbmail**不支持无内容的电子邮件。 若要发送电子邮件，必须指定至少一个 **@body** ，  **@query** ，  **@file_attachments** ，或 **@subject**. 否则为**sp_send_dbmail**返回错误。  
  
 数据库邮件使用当前用户的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 安全上下文控制对文件的访问。 因此，使用进行身份验证的用户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证无法附加文件使用 **@file_attachments** 。 Windows 不允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 从一台远程计算机向另一台远程计算机提供凭据。 所以，如果从运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机以外的计算机运行该命令，则数据库邮件可能无法从网络共享附加文件。  
  
 如果这两个 **@query** 和 **@file_attachments** 指定和找不到该文件，仍执行查询，但不是会发送电子邮件。  
  
 指定查询后，结果集的格式被设置为内联文本。 使用十六进制格式发送结果中的二进制数据。  
  
 参数 **@recipients** ，  **@copy_recipients** ，和 **@blind_copy_recipients** 是以分号分隔的电子邮件地址的列表。 必须提供至少其中一个参数，或**sp_send_dbmail**返回错误。  
  
 在执行时**sp_send_dbmail**事务上下文，数据库邮件启动而无需提交的隐式事务。 在执行时**sp_send_dbmail**从在现有事务，数据库邮件依赖于用户提交或回滚任何更改。 它不会启动内部事务。  
  
## <a name="permissions"></a>权限  
 执行权限**sp_send_dbmail**到的所有成员的默认**DatabaseMailUser**中的数据库角色**msdb**数据库。 但是，当发送消息的用户没有权限请求，使用配置文件**sp_send_dbmail**返回一个错误并且不发送消息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-sending-an-e-mail-message"></a>A. 发送电子邮件  
 此示例将一封电子邮件发送到您使用的电子邮件地址的朋友`myfriend@Adventure-Works.com`。 该邮件的主题为 `Automated Success Message`。 邮件正文包含一句话 `'The stored procedure finished successfully'`。  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @body = 'The stored procedure finished successfully.',  
    @subject = 'Automated Success Message' ;  
```  
  
### <a name="b-sending-an-e-mail-message-with-the-results-of-a-query"></a>B. 发送包含查询结果的电子邮件  
 此示例将一封电子邮件发送到您使用的电子邮件地址的朋友`yourfriend@Adventure-Works.com`。 该邮件的主题为 `Work Order Count`，并执行查询以显示 `DueDate` 在 2004 年 4 月 30 日后的两日内的工单数。 数据库邮件将该结果附加为文本文件。  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @query = 'SELECT COUNT(*) FROM AdventureWorks2012.Production.WorkOrder  
                  WHERE DueDate > ''2004-04-30''  
                  AND  DATEDIFF(dd, ''2004-04-30'', DueDate) < 2' ,  
    @subject = 'Work Order Count',  
    @attach_query_result_as_file = 1 ;  
```  
  
### <a name="c-sending-an-html-e-mail-message"></a>C. 发送 HTML 电子邮件  
 此示例将一封电子邮件发送到您使用的电子邮件地址的朋友`yourfriend@Adventure-Works.com`。 邮件的主题为 `Work Order List`，并包含一个 HTML 文档，其中列出了 `DueDate` 在 2004 年 4 月 30 日后的二日内的工单数。 数据库邮件使用 HTML 格式发送该邮件。  
  
```  
DECLARE @tableHTML  NVARCHAR(MAX) ;  
  
SET @tableHTML =  
    N'<H1>Work Order Report</H1>' +  
    N'<table border="1">' +  
    N'<tr><th>Work Order ID</th><th>Product ID</th>' +  
    N'<th>Name</th><th>Order Qty</th><th>Due Date</th>' +  
    N'<th>Expected Revenue</th></tr>' +  
    CAST ( ( SELECT td = wo.WorkOrderID,       '',  
                    td = p.ProductID, '',  
                    td = p.Name, '',  
                    td = wo.OrderQty, '',  
                    td = wo.DueDate, '',  
                    td = (p.ListPrice - p.StandardCost) * wo.OrderQty  
              FROM AdventureWorks.Production.WorkOrder as wo  
              JOIN AdventureWorks.Production.Product AS p  
              ON wo.ProductID = p.ProductID  
              WHERE DueDate > '2004-04-30'  
                AND DATEDIFF(dd, '2004-04-30', DueDate) < 2   
              ORDER BY DueDate ASC,  
                       (p.ListPrice - p.StandardCost) * wo.OrderQty DESC  
              FOR XML PATH('tr'), TYPE   
    ) AS NVARCHAR(MAX) ) +  
    N'</table>' ;  
  
EXEC msdb.dbo.sp_send_dbmail @recipients='yourfriend@Adventure-Works.com',  
    @subject = 'Work Order List',  
    @body = @tableHTML,  
    @body_format = 'HTML' ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)   
 [sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
  
