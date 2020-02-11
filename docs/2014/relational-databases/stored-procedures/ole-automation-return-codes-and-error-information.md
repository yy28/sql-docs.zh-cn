---
title: OLE 自动化返回代码和错误信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- return codes [SQL Server]
- OLE Automation [SQL Server], return codes
- OLE Automation [SQL Server], errors
ms.assetid: 9696fb05-e9e8-4836-b359-d4de0be0eeb2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34744bedb701155d2695f6efc5aab3c493e6cf48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63011262"
---
# <a name="ole-automation-return-codes-and-error-information"></a>OLE 自动化返回代码和错误信息
  OLE 自动化系统存储过程返回一个 `int` 返回代码，该代码是基础 OLE 自动化操作返回的 HRESULT。 HRESULT 为 0 表示成功。 非零 HRESULT 是十六进制形式 0x800*nnnnn*的 OLE 错误代码，但在存储过程返回代码中`int`作为值返回时，HRESULT 的形式为 214*nnnnnnn*。  
  
 例如，传递无效对象名称（SQLDMO）。Sqldmo.xyzzy）到 sp_OACreate 会导致过程返回2147221005的`int` HRESULT，这是0x800401f3 的十六进制。  
  
 可以使用 `CONVERT(binary(4), @hresult)` 将 `int` HRESULT 转换为 `binary` 值。 但是，使用 `CONVERT(char(10), CONVERT(binary(4), @hresult))` 将产生一个不可读的字符串，因为 HRESULT 的每个字节都被转换成一个 ASCII 字符。 您可以使用以下示例 HexToChar 存储过程将`int` HRESULT 转换为包含可读`char`十六进制字符串的值。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT name FROM sys.objects  
          WHERE name = N'dbo.sp_HexToChar')  
    DROP PROCEDURE HexToChar;  
GO  
CREATE PROCEDURE dbo.sp_HexToChar  
    @BinValue varbinary(255),  
    @HexCharValue nvarchar(255) OUTPUT  
AS  
    DECLARE @CharValue nvarchar(255);  
    DECLARE @Position int;  
    DECLARE @Length int;  
    DECLARE @HexString nchar(16);  
    SELECT @CharValue = N'0x';  
    SELECT @Position = 1;  
    SELECT @Length = DATALENGTH(@BinValue);  
    SELECT @HexString = N'0123456789ABCDEF';  
    WHILE (@Position <= @Length)  
    BEGIN  
        DECLARE @TempInt int;  
        DECLARE @FirstInt int;  
        DECLARE @SecondInt int;  
        SELECT @TempInt = CONVERT(int, SUBSTRING(@BinValue,@Position,1));  
        SELECT @FirstInt = FLOOR(@TempInt/16);  
        SELECT @SecondInt = @TempInt - (@FirstInt*16);  
        SELECT @CharValue = @CharValue +  
            SUBSTRING(@HexString, @FirstInt+1, 1) +  
            SUBSTRING(@HexString, @SecondInt+1, 1);  
        SELECT @Position = @Position + 1;  
    END  
    SELECT @HexCharValue = @CharValue;  
GO  
DECLARE @BinVariable varbinary(35);  
DECLARE @CharValue nvarchar(35);  
  
SET @BinVariable = 123456;  
  
EXECUTE dbo.sp_HexToChar  
    @binvalue = @BinVariable,  
    @HexCharValue = @CharValue OUTPUT;  
  
SELECT @BinVariable AS BinaryValue,  
    @CharValue AS CharacterRep;  
GO  
```  
  
 当其中一个 OLE 自动化过程返回非零的 HRESULT 返回代码时，可以使用以下示例存储过程 **sp_displayoaerrorinfo** 显示 OLE 自动化错误信息。 此示例存储过程使用`HexToChar`。  
  
```  
CREATE PROCEDURE dbo.sp_DisplayOAErrorInfo  
    @Object int,  
    @HResult int  
AS  
    DECLARE @Output nvarchar(255);  
    DECLARE @HRHex nchar(10);  
    DECLARE @HR int;  
    DECLARE @Source nvarchar(255);  
    DECLARE @Description nvarchar(255);  
    PRINT N'OLE Automation Error Information';  
    EXEC HexToChar @HResult, @HRHex OUT;  
    SELECT @Output = N'  HRESULT: ' + @HRHex;  
    PRINT @Output;  
    EXEC @HR = sp_OAGetErrorInfo  
        @Object,  
        @Source OUT,  
        @Description OUT;  
    IF @HR = 0  
    BEGIN  
        SELECT @Output = N'  Source: ' + @Source;  
        PRINT @Output;  
        SELECT @Output = N'  Description: '  
               + @Description;  
        PRINT @Output;  
    END  
    ELSE  
    BEGIN  
       PRINT N' sp_OAGetErrorInfo failed.';  
       RETURN;  
    END  
GO  
```  
  
## <a name="related-content"></a>相关内容  
 [sp_OAGetErrorInfo (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql)  
  
  
