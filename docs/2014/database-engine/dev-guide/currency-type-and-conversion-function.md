---
title: 货币类型和转换函数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: df516567-8689-45c2-b418-16473f8d43e4
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f4c3aae27950cdaa6ff2244abdc2de501c0b1f2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332477"
---
# <a name="currency-type-and-conversion-function"></a>Currency 类型和转换函数
  此示例使用 C# 定义 Currency 用户定义数据类型。 此用户定义数据类型封装了金额和区域，区域有助于确定一种正确的方式，以便将金额以该区域的货币值呈现。 此示例还提供了返回 Currency 用户定义数据类型实例的货币转换函数。 如果 AdventureWorks 数据库包含从美元 (USD) 到与指定区域关联的货币的换算比率，那么转换函数返回的 Currency 用户定义数据类型中包含换算的比率以及与请求的区域相匹配的区域。 否则，返回的 Currency 用户定义数据类型包含原始金额（应是 USD）及 `en-us` 区域。 该示例还说明如何使用 Transact-SQL 注册和注销公共语言运行时 (CLR) 方法和程序集。  
  
> [!CAUTION]  
>  此示例中使用的汇率是虚构的，不能用于实际金融交易。  
  
## <a name="prerequisites"></a>必要條件  
 若要创建和运行此项目，必须安装下列软件：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 可以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 文档和示例[网站](http://go.microsoft.com/fwlink/?LinkId=31046)免费获取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]开发人员[网站](http://go.microsoft.com/fwlink/?linkid=62796)提供的 AdventureWorks 数据库  
  
-   .NET Framework SDK 2.0 或更高版本，或 Microsoft Visual Studio 2005 或更高版本。 您可以免费获取 .NET Framework SDK。  
  
-   此外，还必须满足以下条件：  
  
-   使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例必须已启用 CLR 集成。  
  
-   若要启用 CLR 集成，请执行以下步骤：  
  
    #### <a name="enabling-clr-integration"></a>启用 CLR 集成  
  
    -   执行以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令：  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  若要启用 CLR，必须具有`ALTER SETTINGS`服务器级权限，其中的成员隐式拥有`sysadmin`和`serveradmin`固定服务器角色的成员。  
  
-   必须在您使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上安装 AdventureWorks 数据库。  
  
-   如果你不是管理员[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在使用的实例，必须让管理员授予您**CreateAssembly**权限，才能完成安装。  
  
## <a name="building-the-sample"></a>生成示例  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>按照以下说明创建和运行该示例：  
  
1.  打开 Visual Studio 或 .NET Framework 命令提示符。  
  
2.  如有必要，为您的示例创建目录。 对于此示例，我们将使用 C:\MySample。  
  
3.  在 c:\MySample 中，创建 `Currency.cs` 并将 C# 示例代码（如下所示）复制到该文件中。  
  
4.  从命令行提示符的示例代码执行来编译：  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll  /target:library Currency.cs`  
  
5.  将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安装代码复制到一个文件中，并在示例目录中将其另存为 `Install.sql`。  
  
6.  如果示例安装在 `C:\MySample\` 之外的目录中，请按说明编辑文件 `Install.sql` 以指向该位置。  
  
7.  通过执行以下命令部署程序集和存储过程：  
  
    -   `sqlcmd -E -I -i install.sql`  
  
8.  复制[!INCLUDE[tsql](../../includes/tsql-md.md)]到一个文件测试命令脚本并将其保存为`test.sql`示例目录中。  
  
9. 使用以下命令执行测试脚本：  
  
    -   `sqlcmd -E -I -i test.sql`  
  
10. 将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 清除脚本复制到一个文件中，并在示例目录中将其另存为 `cleanup.sql`。  
  
11. 使用以下命令执行该脚本：  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>示例代码  
 下面是此示例的代码列表。  
  
 C#  
  
```  
using System;  
using System.Globalization;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Data;  
using System.Data.Sql;  
using System.IO;  
using System.Data.SqlClient;  
  
    /// <summary>  
    ///Defines a class for handing particular amounts of money in a   
    ///particular culture's monetary system.  This class is exposed as   
    ///a SQL Server UDT.  
///   
///Note that we are implementing IComparable to affect comparison behavior   
///only within the CLR.  This does not affect how SQL Server will compare the  
///     the types.  How SQL Server will compare the type is determined by the Write   
///method on IBinarySerialize.  
    /// </summary>  
[Serializable]  
    [SqlUserDefinedType(Format.UserDefined, IsByteOrdered = true, MaxByteSize = 32)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
        const string nullMarker = "\0\0\0\0\0\0\0\0\0\0";  
        const int cultureNameMaxSize = 10;  
  
        private string cultureName;//Who issued the money (en-us, for example)  
  
        private CultureInfo culture;//The object which represents cultureName  
  
        private decimal currencyValue;//The amount of money  
  
        // Public properties for private fields  
        public CultureInfo Culture  
        {  
            get  
            {  
                //A culture name is required.  If not present the entire object is considered null.  
                if (cultureName == null) return null;  
  
                //If we've got a cached copy of the culture return it.  
                if (culture != null) return culture;  
  
                //Otherwise, set the cache and return the culture for the culture name specified.  
                culture = CultureInfo.CreateSpecificCulture(cultureName);  
                return culture;  
            }  
        }  
  
        // Public property for the private field.  
        public decimal CurrencyValue  
        {  
            get  
            {  
                return currencyValue;  
            }  
        }  
  
        // Constructors for when we have the culture or the name of the culture  
  
        public Currency(CultureInfo culture, decimal currencyValue)  
        {  
if (culture == null) throw new ArgumentNullException("culture");  
            this.cultureName = culture.Name;  
            this.culture = culture;  
            this.currencyValue = currencyValue;  
        }  
  
        public Currency(string cultureName, decimal currencyValue)  
        {  
            this.cultureName = cultureName;  
            this.culture = null;  
            this.currencyValue = currencyValue;  
        }  
  
        //Return the string representation for the currency, including the currency symbol.  
        [SqlMethod(IsDeterministic = true,  
            IsPrecise = true, DataAccess = DataAccessKind.None,  
            SystemDataAccess = SystemDataAccessKind.None)]  
        public override string ToString()  
        {  
            if (this.Culture == null) return "null";  
  
            return String.Format(this.Culture, "{0:c}", currencyValue);  
        }  
  
        //The entire value of the currency is considered null if the culture name is null  
        public bool IsNull  
        {  
            get  
            {  
                return cultureName == null;  
            }  
        }  
  
        //The no-argument constructor makes a null currency.  
        public static Currency Null  
        {  
            get  
            {  
                Currency h = new Currency((String)null, 0);  
  
                return h;  
            }  
        }  
  
        //Be sure to set the current UI culture before using this method! Even better, provide the culture  
        //specifically (for the method after this one).  
        [SqlMethod(IsDeterministic = true, IsPrecise = true, DataAccess = DataAccessKind.None, SystemDataAccess = SystemDataAccessKind.None)]  
        public static Currency Parse(SqlString sqlString)  
        {  
            return ParseWithCulture(sqlString, CultureInfo.CurrentUICulture);  
        }  
  
        public static Currency ParseWithCulture(SqlString sqlString, CultureInfo culture)  
        {  
            if (sqlString.IsNull   
|| (string.Compare(sqlString.Value, "null", true, CultureInfo.CurrentUICulture) == 0))  
                return Currency.Null;  
  
            int digitPos = -1;  
            string stringValue = sqlString.Value;  
  
            while (digitPos < stringValue.Length   
                && !Char.IsDigit(stringValue, ++digitPos))  
            {  
            }  
  
            if (digitPos < stringValue.Length)  
                return new Currency(culture, decimal.Parse(  
                    stringValue.Substring(digitPos), culture));  
  
            return Currency.Null;  
        }  
  
        public override int GetHashCode()  
        {  
            if (this.IsNull)  
                return 0;  
  
            return this.ToString().GetHashCode();  
        }  
  
//Note: This only affects the behavior of CLR, not SQL Server.  Comparisions  
//for SQL Server will be determined by the Write method below.  
  
public int CompareTo(object obj)  
        {  
            if (obj == null)  
                return 1; //by definition  
  
            if (obj == null || !(obj is Currency))  
                throw new ArgumentException(  
                    "the argument to compare is not a Currency");  
  
            Currency c = (Currency)obj;  
  
            if (this.IsNull)  
            {  
                if (c.IsNull)  
                    return 0;  
  
                return -1;  
            }  
  
            if (c.IsNull)  
                return 1;  
  
            string thisCultureName = this.Culture.Name;  
            string otherCultureName = c.Culture.Name;  
            if (!thisCultureName.Equals(otherCultureName))  
                return thisCultureName.CompareTo(otherCultureName);  
            return this.CurrencyValue.CompareTo(c.CurrencyValue);  
        }  
        // IBinarySerialize methods  
        // The binary layout is as follow:  
        //    Bytes 0 - 19:Culture name, padded to the right with null characters, UTF-16 encoded  
        //    Bytes 20+:Decimal value of money  
        // If the culture name is empty, the currency is null.  
  
        public void Write(System.IO.BinaryWriter w)  
        {  
if (w == null) throw new ArgumentNullException("w");  
            if (this.IsNull)  
            {  
                w.Write(nullMarker);  
                w.Write((decimal)0);  
                return;  
            }  
  
            if (cultureName.Length > cultureNameMaxSize)  
            {  
                throw new ApplicationException(string.Format(  
                    CultureInfo.InvariantCulture,   
                    "{0} is an invalid culture name for currency as it is too long.",   
                    cultureNameMaxSize));  
            }  
  
            String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
            for (int i = 0; i < cultureNameMaxSize; i++)  
            {  
                w.Write(paddedName[i]);  
            }  
  
            // Normalize decimal value to two places  
            currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
            w.Write(currencyValue);  
        }  
        public void Read(System.IO.BinaryReader r)  
        {  
            char[] name = r.ReadChars(cultureNameMaxSize);  
            int stringEnd = Array.IndexOf(name, '\0');  
  
            if (stringEnd == 0)  
            {  
                cultureName = null;  
                return;  
            }  
  
            cultureName = new String(name, 0, stringEnd);  
            currencyValue = r.ReadDecimal();  
        }  
    }  
  
    /// <summary>  
    /// This class is used to compute the value of US money a given region.  
    /// </summary>  
    public sealed class CurrencyConverter  
    {  
        // Classes with only static members should not be instantiable  
        private CurrencyConverter()  
        {  
        }  
  
        private static readonly CultureInfo USCulture = CultureInfo.CreateSpecificCulture("en-us");  
  
        /// <summary>  
        ///Computes the value of a certain amount of money in the USA in a different region.  
        /// </summary>  
        /// <param name="fromAmount">The quantity of money</param>  
        /// <param name="toCultureName">A culture which is a member of the region of interest</param>  
        /// <returns></returns>  
        [Microsoft.SqlServer.Server.SqlFunction(IsDeterministic = true, DataAccess = Microsoft.SqlServer.Server.DataAccessKind.Read)]  
        public static Currency ConvertCurrency(SqlMoney fromAmount, SqlString toCultureName, SqlDateTime when)  
        {  
            CultureInfo toCulture = CultureInfo.CreateSpecificCulture(toCultureName.Value);  
  
            if (toCulture.Equals(USCulture))  
            {  
                Currency c = new Currency(USCulture, (decimal)fromAmount);  
                return c;  
            }  
  
            String toCurrencyCode = new RegionInfo(toCulture.LCID).ISOCurrencySymbol;  
  
            // Find the rate closest to the specified date  
  
            using (SqlConnection conn = new SqlConnection("context connection=true"))  
            {  
  
                SqlCommand command = conn.CreateCommand();  
                command.CommandType = CommandType.StoredProcedure;  
                command.CommandText = "usp_LookupConversionRate";  
  
                SqlParameter onDateParameter  
                    = new SqlParameter("@OnDate", SqlDbType.DateTime);  
                onDateParameter.Value = when;  
                command.Parameters.Add(onDateParameter);  
  
                SqlParameter toCurrencyCodeParameter  
                    = new SqlParameter("@ToCurrencyCode", SqlDbType.NChar, 3);  
                toCurrencyCodeParameter.Value = toCurrencyCode;  
                command.Parameters.Add(toCurrencyCodeParameter);  
  
                SqlParameter resultParameter  
                    = new SqlParameter("@Result", SqlDbType.Decimal);  
                resultParameter.Precision = 10;  
                resultParameter.Scale = 4;  
                resultParameter.Direction = ParameterDirection.Output;  
                command.Parameters.Add(resultParameter);  
  
                conn.Open();  
                command.ExecuteNonQuery();  
  
                decimal conversionFactor;  
  
                if (resultParameter.Value is decimal)  
                {  
                    conversionFactor = (decimal)(resultParameter.Value);  
                }  
                else  
                {  
                    conversionFactor = 1.0M;  
                    toCulture = USCulture;  
                }  
  
                return new Currency(toCulture, ((decimal)fromAmount * conversionFactor));  
            }  
        }  
    }  
```  
  
 这是[!INCLUDE[tsql](../../includes/tsql-md.md)]安装脚本 (`Install.sql`)，它将程序集部署并在数据库中创建存储的过程。  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_LookupConversionRate')  
DROP PROCEDURE [dbo].[usp_LookupConversionRate]  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE [name] = N'Currency')   
DROP TYPE Currency;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'Currency')  
DROP ASSEMBLY Currency;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE ([name] = N'ConvertCurrency') AND ([type] = 'FS'))  
DROP FUNCTION ConvertCurrency;  
GO  
  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
DECLARE @SamplesPath nvarchar(1024)  
set @SamplesPath = 'C:\MySample\'  
CREATE ASSEMBLY Currency   
FROM @SamplesPath + 'Currency.dll'  
with permission_set = safe;  
  
USE AdventureWorks  
GO  
  
CREATE TYPE Currency EXTERNAL NAME [Currency].[Currency];  
GO  
  
CREATE FUNCTION ConvertCurrency  
(  
@fromAmount AS money,  
@toCultureName AS nvarchar(10),  
@when as DateTime  
)  
RETURNS Currency  
AS EXTERNAL NAME [Currency].[CurrencyConverter].ConvertCurrency;  
GO  
  
CREATE PROCEDURE usp_LookupConversionRate  
(  
@OnDate datetime,  
@ToCurrencyCode nchar(3),  
@Result decimal(10,4) OUTPUT  
)  
AS  
BEGIN  
--It is not permitted to perform certain side-effects in functions, and  
--SET NOCOUNT is one of them.  Since this sproc is called from   
--the ConvertCurrency CLR UDF, we must not do that side-effect or  
--there will be an error at runtime.  
--SET NOCOUNT ON  
  
SELECT @Result = (SELECT TOP 1 AverageRate FROM Sales.CurrencyRate   
WHERE CurrencyRateDate <= @OnDate AND FromCurrencyCode = N'USD'   
AND ToCurrencyCode = @ToCurrencyCode   
ORDER BY CurrencyRateDate DESC);  
  
IF (@Result IS NULL)  
SELECT @Result = (SELECT TOP 1 AverageRate FROM Sales.CurrencyRate   
WHERE CurrencyRateDate > @OnDate AND FromCurrencyCode = N'USD'   
AND ToCurrencyCode = @ToCurrencyCode  
ORDER BY CurrencyRateDate ASC);  
END;  
  
```  
  
 这是 `test.sql`，该脚本通过执行函数测试该示例。  
  
```  
use AdventureWorks  
GO  
  
DECLARE @TwoBitsEuro Currency;  
SELECT @TwoBitsEuro = dbo.ConvertCurrency(CAST('.25' as money), 'FR-FR', GetDate());  
PRINT '$0.25 in USD is equivalent to ' + @TwoBitsEuro.ToString();  
```  
  
 下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 从数据库中删除程序集、类型和函数。  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_LookupConversionRate')  
DROP PROCEDURE [dbo].[usp_LookupConversionRate]  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [公共语言运行时 (CLR) 集成的使用方案和示例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
