---
title: "添加 Transact-SQL 代码段 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 901c7995-8eb5-4d12-8bb0-de0a922b48f8
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2498e15c9927adde026e426ead756be389ce08d1
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="add-transact-sql-snippets"></a>添加 Transact-SQL 代码段
  您可以将自己的 Transact-SQL 代码段添加到在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中包括的一组预定义的代码段中。  
  
## <a name="creating-a-transact-sql-snippet-file"></a>创建 Transact-SQL 代码段文件  
 创建 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码段的第一步是创建具有您的代码段文本的 XML 文件。 该文件必须具有 .snippet 文件扩展名，并且必须满足 [代码段架构](http://go.microsoft.com/fwlink/?LinkId=207504)的要求。 将代码段语言设置为 SQL。  
  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 随附的预定义代码段作为示例。 若要找到预定义的代码段，请打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，选择“工具”菜单，然后单击“代码段管理器”。 在 **“语言”** 列表框中选择 **SQL** ，指向 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码段的路径将显示在 **“位置”** 框中。  
  
## <a name="registering-the-code-snippet"></a>注册代码段  
 在创建代码段文件后，使用代码段管理器向 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]注册该代码段。 您可以添加包含多个代码段的文件夹，或者将单独的代码段导入到 **“我的代码段”** 文件夹中。  
  
## <a name="procedures"></a>过程  
  
#### <a name="adding-a-snippet-folder"></a>添加代码段文件夹  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  选择 **“工具”** 菜单，然后单击 **“代码段管理器”**。  
  
3.  单击 **“添加”** 按钮。  
  
4.  导航到包含您的代码段的文件夹，然后单击 **“选择文件夹”** 按钮。  
  
#### <a name="importing-a-snippet"></a>导入代码段  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  选择 **“工具”** 菜单，然后单击 **“代码段管理器”**。  
  
3.  单击 **“导入”** 按钮。  
  
4.  导航到包含您的代码段的文件夹，单击 .snippet 文件，然后单击 **“打开”** 按钮。  
  
## <a name="examples"></a>示例  
 以下示例将创建一个 **TRY-CATCH** 外侧代码段，然后将其导入到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中。  
  
1.  将以下代码粘贴到记事本，然后将其另存为名为 TryCatch.snippet 的文件。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
    <_locDefinition xmlns="urn:locstudio">  
        <_locDefault _loc="locNone" />  
        <_locTag _loc="locData">Title</_locTag>  
        <_locTag _loc="locData">Description</_locTag>  
        <_locTag _loc="locData">Author</_locTag>  
        <_locTag _loc="locData">ToolTip</_locTag>  
       <_locTag _loc="locData">Default</_locTag>  
    </_locDefinition>  
    <CodeSnippet Format="1.0.0">  
    <Header>  
    <Title>TryCatch</Title>  
                            <Shortcut></Shortcut>  
    <Description>Example Snippet for Try-Catch.</Description>  
    <Author>SQL Server Books Online Example</Author>  
    <SnippetTypes>  
                                    <SnippetType>SurroundsWith</SnippetType>  
    </SnippetTypes>  
    </Header>  
    <Snippet>  
    <Declarations>  
                                    <Literal>  
                                    <ID>CatchCode</ID>  
                                    <ToolTip>Code to handle the caught error</ToolTip>  
                                    <Default>CatchCode</Default>  
                                    </Literal>  
    </Declarations>  
    <Code Language="SQL"><![CDATA[  
    BEGIN TRY  
  
    $selected$ $end$  
  
    END TRY  
    BEGIN CATCH  
  
    $CatchCode$  
  
    END CATCH;  
    ]]>  
    </Code>  
    </Snippet>  
    </CodeSnippet>  
    </CodeSnippets>  
    ```  
  
2.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
3.  选择 **“工具”** 菜单，然后单击 **“代码段管理器”**。  
  
4.  单击 **“导入”** 按钮。  
  
5.  导航到包含 TryCatch.snippet 的文件夹，单击该 TryCatch.snippet 文件，然后单击 **“打开”** 按钮。 您不应在 **“我的代码段”** 文件夹中具有 TryCatch 代码段。  
  
## <a name="see-also"></a>另请参阅  
 [插入外侧 Transact-SQL 代码段](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
