---
title: 允许部分受信任的调用方 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- AllowPartiallyTrustedCallers attribute
- security [CLR integration]
- common language runtime [SQL Server], security
- partially trusted callers [CLR integration]
ms.assetid: 20b0248f-36da-4fc3-97d2-3789fcf6e084
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bed854ba13bec4206f3ee869795af91c4da4f525
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754195"
---
# <a name="allowing-partially-trusted-callers"></a>允许部分可信任的调用方
  对于公共语言运行时 (CLR) 集成而言，共享代码库是一种常见方案。其中包含用户定义类型、存储过程、用户定义函数、用户定义聚合、触发器或实用工具类的程序集通常可由另一个程序集或应用程序进行访问。 要由多个应用程序共享的代码库必须使用强名称进行签名。  
  
 只有运行时代码访问安全性系统完全信任的应用程序才允许访问未用 `System.Security.AllowPartiallyTrustedCallers` 属性显式标记的共享托管代码程序集。 在未使用此属性的情况下，部分可信任的程序集（即在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用 `SAFE` 或 `EXTERNAL_ACCESS` 权限集注册的程序集）尝试访问使用强名称签名的程序集时，会导致引发 `System.Security.SecurityException` 异常。 您会看到如下错误消息：  
  
```  
Msg 6522, Level 16, State 1, Procedure usp_RSTest, Line 0  
A .NET Framework error occurred during execution of user defined  
routine or aggregate 'usp_RSTest':  System.Security.SecurityException: That assembly does not allow partially trusted callers.  
System.Security.SecurityException: at  
System.Security.CodeAccessSecurityEngine.ThrowSecurityException(  
Assembly asm, PermissionSet granted,PermissionSet refused,  
RuntimeMethodHandle rmh, SecurityAction action, Object demand,  
IPermission permThatFailed) at  
Microsoft.Samples.SqlServer.TestResultSet.Test()  
```  
  
 建议所有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册的程序集（添加到全局程序集缓存中的那些程序集除外）使用 `AllowPartiallyTrustedCallers` 属性进行标记，以便由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 加载的程序集可以相互访问。 应当首先彻底检查要加载到全局程序集缓存中的程序集的安全性，然后再添加 `AllowPartiallyTrustedCallers` 属性，因为之后该程序集将可用于来自意外上下文的部分可信任的调用方。 程序集不应注册为完全可信任（在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用 `UNSAFE` 权限集注册）。  
  
 有关详细信息，请参阅 .NET Framework 软件开发包中的“通过部分可信任的代码使用库”部分。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 假设有一个实用工具类对许多服务器端 CLR 集成应用程序都非常有用。 例如，它可能是一个表示查询调用结果的类。 若要启用对此组件的共享，请将此实用工具类置于单独的程序集中。 然后，即可从包含 CLR 集成对象的各种其他程序集引用该程序集。 因为此实用工具类可用于多个不同的服务器应用程序，所以应仔细检查并解决任何安全问题。 然后，将 `AllowPartiallyTrustedCallers` 属性应用于包含此实用工具类的程序集，以便通过 `SAFE` 或 `EXTERNAL_ACCESS` 权限集标记的程序集中包含的 CLR 集成对象可以使用此实用工具类和方法，即使此实用工具类和方法位于单独的程序集中。  
  
 有时，在通读查询结果时能够执行命令（而不需要打开新的连接并将所有结果读入内存）很有用。 ADO.NET 2.0 中的多个活动的结果集 (MARS) 功能就是一种能够帮助您实现以上操作的技术。 目前，用于服务器端编程的进程内的提供程序不能实现 MARS。 若要消除此限制，可以使用服务器端游标。 此示例说明如何使用服务器端游标解决对服务器端编程缺少 MARS 支持的问题。  
  
 使用服务器端游标要消耗大量的服务器资源，并且有时会阻碍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的查询优化器增强查询的性能。 因此，可以考虑重新编写代码来尽可能使用 JOIN。  
  
 除了可以在结果集中前后移动以外，此类的 API 与数据读取器相似，即使结果集处于打开状态时，也可以在连接时发出其他命令。  
  
 大大简化了此实现过程，以便使该示例易于理解。 更有效的实现将提取多行来避免提取的每行的数据库周转。  
  
 与用查询的所有结果填充数据集比较，使用此类可以大大减少内存需求量，这对于服务器端编程是非常重要的。  
  
 此示例还说明如何使用“允许部分受信任的调用方”属性来指示结果集程序集是可以安全地从其他程序集进行调用的库。 与使用不安全的权限注册调用程序集相比，此方法稍微复杂一些，但要安全许多。 该方法更安全的原因是：它将调用程序集注册为安全的程序集，调用程序集将限制相关资源脱离服务器并防止对服务器的完整性造成损害。  
  
 此示例的生成说明假定源代码文件位于名为 c:\samples 的目录中。  如果您使用另一个目录，则必须修改 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。 [!INCLUDE[tsql](../../includes/tsql-md.md)]脚本还需要 AdventureWorks 数据库。 可以从 " [Microsoft SQL Server 示例和社区项目](https://go.microsoft.com/fwlink/?LinkID=85384)" 主页下载 AdventureWorks 示例数据库。  
  
 若要生成和运行该示例，将第一个代码列表粘贴到名为 ResultSet.cs 的文件中，并使用 csc /target:library ResultSet.cs 进行编译。  
  
 将第二个代码列表粘贴到名为 TestResultSet.cs 的文件中，并使用 csc /target:library /reference:ResultSet.dll TestResultSet.cs 进行编译。  
  
 将第三个代码列表粘贴到名为 InstallCS.sql 的文件中，并使用 sqlcmd-E-I-i InstallCS.sql 进行编译。  
  
 将第四个代码列表粘贴到名为 test.sql 的文件中，并使用 sqlcmd -E -I -i test.sql 进行编译。  
  
 将第五个代码列表粘贴到名为 Cleanup.sql 的文件中，并使用 sqlcmd -E -I -i Cleanup.sql 进行编译。  
  
### <a name="code"></a>代码  
  
```  
// ResultSet.cs  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.Common;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using System.IO;  
using System.Globalization;  
using Microsoft.SqlServer.Server;  
using System.Runtime.Serialization;  
  
[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "Microsoft.Samples.SqlServer")]  
[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", Scope = "member", Target = "Microsoft.Samples.SqlServer.ResultSetEnumerator.System.Collections.IEnumerator.Current", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
  
namespace Microsoft.Samples.SqlServer {  
   // This is the base class for exceptions raised in the Adventure Works Cycles Storefront application.  
   [Serializable]  
   public class ResultSetException : System.Exception {  
      public ResultSetException() {}  
      public ResultSetException(string message) : base(message) {}  
      public ResultSetException(String message, Exception innerException) : base(message, innerException) {}  
      protected ResultSetException(SerializationInfo info, StreamingContext context) : base(info, context) {}  
   }  
  
   // This exception is raised when a user tries to register an email address which has already been taken.  
   [Serializable]  
   public class InvalidStateException : ResultSetException {  
      public InvalidStateException() {}  
      public InvalidStateException(string message) : base(message) {}  
      public InvalidStateException(String message, Exception innerException) : base(message, innerException) {}  
      protected InvalidStateException(SerializationInfo info, StreamingContext context) : base(info, context) {}  
   }  
  
   // This class is used to provide an API similar to a SQL data reader except that it is possible to navigate through any   
   // part of the result set.  It is also possible to execute commands while this class is still "open" even though the   
   // CLR in-proc provider does not support MARS at this time. This implementation is highly simplified to make the   
   // sample easy to understand.  A better implementation would fetch multiple rows to avoid a database turnaround per row   
   // fetched.  Using this class can have a significantly smaller memory footprint than filling a dataset with   
   // all the results of a query which is very important for server side programming.  
   [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1010:CollectionsShouldImplementGenericInterface"), System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Naming", "CA1710:IdentifiersShouldHaveCorrectSuffix")]  
   public class ResultSet : IDataReader, IDataRecord, IEnumerable, IDisposable {  
      // Which database to access  
      private SqlConnection connection;  
  
      // A cache or a single row's worth of data   
      private Microsoft.SqlServer.Server.SqlDataRecord results;  
  
      //A cache of whether the columns of the current cached row are set to the default value for the column  
      private int visibleFieldCount;  
  
      private string cursorName = string.Format(CultureInfo.InvariantCulture, "[{0}]", Guid.NewGuid().ToString());  
  
      internal Microsoft.SqlServer.Server.SqlDataRecord CurrentRecord {  
         get {  
            EnsureState(StateValues.read);  
            return results;  
         }  
      }  
  
      // Which database to access.  The connection passed to the setter must be open.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")/*, System.CLSCompliant(false)*/]  
      public SqlConnection Connection {  
         get {  
            return connection;  
         }  
  
         set {  
            if (value == null)  
               throw new ArgumentNullException("value");  
            if (state != StateValues.created && state != StateValues.initialized)  
               throw new InvalidStateException("Cannot alter select command after opening the result set.");  
            if (value.State != ConnectionState.Open)  
               throw new InvalidStateException("Connection must be opened prior to setting result set connection value.");  
            connection = value;  
            if (selectCommand != null && connection != null)  
               state = StateValues.initialized;  
            else  
               state = StateValues.created;  
         }  
      }  
  
      private string selectCommand;  //What query to execute against the database  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")]  
      public string SelectCommand {  
         get {  
            return selectCommand;  
         }  
  
         set {  
            if (state != StateValues.created && state != StateValues.initialized)  
               throw new InvalidStateException("Cannot alter select command after opening the result set.");  
            selectCommand = value;  
            if (selectCommand != null && connection != null)  
               state = StateValues.initialized;  
            else  
               state = StateValues.created;  
         }  
      }  
  
      private bool isScrollable = true;  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")]  
      public bool IsScrollable {  
         get {  
            return isScrollable;  
         }  
  
         set {  
            if (state != StateValues.created && state != StateValues.initialized)  
               throw new InvalidStateException("Cannot alter IsScrollable property after opening the result set.");  
            isScrollable = value;  
         }  
      }  
  
      // The possible phases this object can go through from creation through termination.  
      // created:  Result set is instantiated but connection and select command are not set  
      // initialized:  Result set is instantiated and connection and select command are set  
      // opened:  The cursor has been created for browsing data  
      // read:  At least one row of data has been read and cached.  
      // closed:  Cursor is closed and deallocated, and connection is closed.  No further operations are possible.  
      private enum StateValues { created, initialized, opened, read, closed };   
  
      // What the current phase is  
      private StateValues state = StateValues.created;  
  
      // It is possible to create the result set with this constructor and then set the connection  
      // and select command using the public properties.  
      public ResultSet() {}  
  
      // Or you can create the result set all at once using this form of the constructor.  
      public ResultSet(SqlConnection connection, string selectCommand) {  
         this.Connection = connection;  
         this.SelectCommand = selectCommand;  
         state = StateValues.initialized;  
      }  
  
      // By default the result set is scrollable, but you can create a forward-only result set using this constructor   
      // and specifying false for isScrollable.  
      public ResultSet(SqlConnection connection, string selectCommand, bool isScrollable) {  
         this.Connection = connection;  
         this.SelectCommand = selectCommand;  
         this.IsScrollable = isScrollable;  
         state = StateValues.initialized;  
      }  
  
      // This method should be called just before the result set is to be used to pull data.  The open doesn't happen as   
      // part of creation as server resources are being consumed while the result set is open.  Be sure to close an open   
      // result set as soon as possible to release server side resources.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")]  
      public void Open() {  
         switch (state) {  
            case StateValues.created:  
               throw new InvalidStateException("Cannot open result set until it is properly initialized");  
            case StateValues.opened:  
            case StateValues.read:  
               throw new InvalidStateException("Result set already open.");  
            case StateValues.closed:  
               throw new InvalidStateException("Cannot reopen closed result set.");  
            default:  
               break;  
         }  
         if (state == StateValues.initialized) {  
            // There are many possible cursor options.  We only allow control of scrollability.  
            // To keep the implementation simple we only permit read operations.  
            string scrollMode = (isScrollable) ? "SCROLL" : "FORWARD_ONLY";  
  
            // Caller must ensure that any user input which is part of selectCommand is free from injection attacks.  
            SqlCommand cmd = connection.CreateCommand();  
            cmd.CommandText = string.Format(CultureInfo.InvariantCulture, "DECLARE {0} CURSOR GLOBAL {1} READ_ONLY  FOR {2}; OPEN {0};",  
                cursorName, scrollMode, selectCommand);  
            cmd.ExecuteNonQuery();  
            state = StateValues.opened;  
         }  
      }  
  
      // Free all server and client side resources being consumed for this result set.  Most operations  
      // are no longer valid after calling this method on the result set.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.InvalidStateException.#ctor(System.String)")]  
      public void Close() {  
         switch (state) {  
            case StateValues.created:  
            case StateValues.initialized:  
               throw new InvalidStateException("Cannot close unopened result set.");  
            case StateValues.closed:  
               throw new InvalidStateException("Result set already closed.");  
            case StateValues.opened:  
            case StateValues.read:  
               SqlCommand cmd = connection.CreateCommand();  
               cmd.CommandText =  
                   string.Format(CultureInfo.InvariantCulture, "CLOSE {0}; DEALLOCATE {0};", cursorName);  
               try {  
                  cmd.ExecuteNonQuery();  
               }  
               finally {  
                  results = null;  
                  state = StateValues.closed;  
               }  
               break;  
            default:  
               throw new InvalidStateException(  
                   string.Format(CultureInfo.InvariantCulture,  
                   "Unknown result set state {0}", state.ToString()));  
         }  
  
      }  
  
      // This implementation does not support multi-dimensional data. Always zero.  
      public int Depth {  
         get {  
            EnsureState(StateValues.read);  
            return 0;  
         }  
      }  
  
      // Normally this would return a data table with schema information about the data being returned.  
      // Unfortunately this isn't implemented in the in-proc provider, so always throw a NYI exception.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.NotImplementedException.#ctor(System.String)")]  
      public DataTable GetSchemaTable() {  
         throw new NotImplementedException("GetSchemaTable is not currently implemented.");  
      }  
  
      // Determines if there is any data to read. True if there is data to read, otherwise false.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.NotImplementedException.#ctor(System.String)")]  
      public bool HasRows {  
         get {  
            throw new NotImplementedException("HasRows is not currently implemented.");  
         }  
      }  
  
      // Determines if the result set is available for use  
      // Returns false if the result set is available for use, otherwise true.  
      public bool IsClosed {  
         get { return state == StateValues.closed; }  
      }  
  
      // Multiple result sets are not supported.  Always throws an invalid operation exception.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
      public bool NextResult() {  
         throw new InvalidOperationException("Multiple result sets are not support for result set class");  
      }  
  
      // Fetches the next row from the result set on the server and makes that data available to the caller.  
      // Returns True if and only if there is data to read.  
      public bool Read() {  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH NEXT FROM {0};", cursorName));  
      }  
  
      // Returns the number of records affected by processing this result set.  This may only be called when the result set  
      // is closed.  Since this implementation supports only read-only access, there can never be any rows affected (always -1).  
      public int RecordsAffected {  
         get {  
            EnsureState(StateValues.closed);  
            return -1;  
         }  
      }  
  
      // Move to a particular record number in the results returned by the query.  Requires a scrollable result set.  
      // Returns True if and only if there is data to read.  
      public bool ReadAbsolute(int position) {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH ABSOLUTE {0} FROM {1};",  
             position, cursorName));  
      }  
  
      // Move to the first result in the results returned by the query and read it.  Requires a scrollable result set.  
      // Returns True if and only if there is data to read.  
      public bool ReadFirst() {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH FIRST FROM {0};", cursorName));  
      }  
  
      // Move to the last result in the results returned by the query and read it.  Requires a scrollable result set.  
      // Returns True if and only if there is data to read.  
      public bool ReadLast() {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH LAST FROM {0};", cursorName));  
      }  
  
      // Move to the immediate prior result in the results returned by the query, and read it.  Requires a scrollable   
      // result set.  Returns True if and only if there is data to read.  
      public bool ReadPrevious() {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH PREVIOUS FROM {0};", cursorName));  
      }  
  
      // Move the specified number of records forward or backward from the current position  
      // in the results returned by the query and read it.  Requires a scrollable result set.  
      /// position is how many records forward or backward. Returns True if and only if there is data to read.  
      public bool ReadRelative(int position) {  
         EnsureScroll();  
         return fetch(string.Format(CultureInfo.InvariantCulture, "FETCH RELATIVE {0} FROM {1};", position, cursorName));  
      }  
  
      // Dispose is idential to closing the result set.  
      public void Dispose() {  
         Dispose(true);  
      }  
  
      protected virtual void Dispose(bool shouldClearManagedResources) {  
         Close();  
         if (shouldClearManagedResources)  
            connection = null;  
      }  
  
      // The number of columns available in the results just read  
      public int FieldCount {  
         get {  
            EnsureState(StateValues.read);  
            return results.FieldCount;  
         }  
      }  
  
      public int VisibleFieldCount {  
         get {  
            EnsureState(StateValues.read);  
            return visibleFieldCount;  
         }  
      }  
  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
      public IDataReader GetData(int i) {  
         throw new InvalidOperationException("GetData is no longer implemented");  
      }  
  
      // What kind of data is acceptable for the specified column  
      public string GetDataTypeName(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetDataTypeName(i);  
      }  
  
      // Returns the object which represents the kind of data which is acceptable for the specified column.  
      public Type GetFieldType(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetFieldType(i);  
      }  
  
      // Returns the symbolic id of the specified column  
      public string GetName(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetName(i);  
      }  
  
      // Given a column name, returns the integer id the column.  
      public int GetOrdinal(string name) {  
         EnsureState(StateValues.read);  
         //Note: this implementation does not deal with all collation and internationalization issues.  
         return results.GetOrdinal(name);  
      }  
  
      // Places all the values contained in the current row into the supplied object array.  The elements  
      // of the array are based on the SQL type system.  
      public int GetSqlValues(object[] values) {  
         EnsureState(StateValues.read);  
         return results.GetSqlValues(values);  
      }  
  
      // Places all the values contained in the current row into the supplied object array.  The   
      // elements of the array are based on the CLR type system.  
      public int GetValues(object[] values) {  
         EnsureState(StateValues.read);  
         return results.GetValues(values);  
      }  
  
      // Accesses the data in the specified column by name  
      public object this[string name] {  
         get {  
            EnsureState(StateValues.read);  
            return results[name];  
         }  
      }  
  
      // Accesses the data in the specified column by numerical id  
      public object this[int i] {  
         get {  
            EnsureState(StateValues.read);  
            return results[i];  
         }  
      }  
  
      // The following methods provide access to column data for the current row as objects using the Sql type system.    
      // The advantage of using this type system is that you can deal very precisely with the database's concept of null.    
      // Also, some types (such as SqlXml) provide more efficient methods of data access than the CLR type system.  
  
      // Access the data in the specified column in the current row as a SqlBinary object  
      public SqlBinary GetSqlBinary(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlBinary(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlBoolean object  
      public SqlBoolean GetSqlBoolean(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlBoolean(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlByte object  
      public SqlByte GetSqlByte(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlByte(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlBytes object  
      public SqlBytes GetSqlBytes(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlBytes(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlChars object  
      public SqlChars GetSqlChars(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlChars(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlDateTime object  
      public SqlDateTime GetSqlDateTime(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlDateTime(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlDecimal object  
      public SqlDecimal GetSqlDecimal(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlDecimal(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlDouble object  
      public SqlDouble GetSqlDouble(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlDouble(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlGuid object  
      public SqlGuid GetSqlGuid(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlGuid(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlInt16 object  
      public SqlInt16 GetSqlInt16(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlInt16(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlInt32 object  
      public SqlInt32 GetSqlInt32(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlInt32(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlInt64 object  
      public SqlInt64 GetSqlInt64(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlInt64(i);  
      }  
  
      // Return schema information for the specified column  
      public Microsoft.SqlServer.Server.SqlMetaData GetSqlMetaData(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlMetaData(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlMoney object  
      public SqlMoney GetSqlMoney(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlMoney(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlSingle object  
      public SqlSingle GetSqlSingle(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlSingle(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlString object  
      public SqlString GetSqlString(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlString(i);  
      }  
  
      // Access the data in the specified column in the current row as a Sql object  
      public object GetSqlValue(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlValue(i);  
      }  
  
      // Access the data in the specified column in the current row as a SqlXml object  
      public SqlXml GetSqlXml(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetSqlXml(i);  
      }  
  
      // The following methods provide access to column data for the current row using the CLR type system.  The advantage   
      // of using these methods is seamless integration with other CLR components.  
  
      // Access the data in the specified column in the current row as a Boolean  
      public bool GetBoolean(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetBoolean(i);  
      }  
  
      // Access the data in the specified column in the current row as a byte   
      public byte GetByte(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetByte(i);  
      }  
  
      // Copies bytes from the specified column of the current row into a buffer supplied by the caller.  
      // i is the columm, fieldOffset is where to start in the column's data, buffer is where to place the bytes,  
      // bufferOffset is where to start in the buffer, and length is how many bytes to copy.    
      // Returns how many bytes were actually copied.  
      public long GetBytes(int i, long fieldOffset, byte[] buffer, int bufferoffset, int length) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetBytes(i, fieldOffset, buffer, bufferoffset, length);  
      }  
  
      // Access the data in the specified column in the current row as a  char.  
      public char GetChar(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetChar(i);  
      }  
  
      // Copies characters from the specified column of the current row into a buffer supplied by the caller.  
      // i is the column, fieldoffset is where to start in the column's data, buffer is where to place the characters,  
      // bufferoffset is where to start in the buffer, length is how many characters to copy.  
      // Returns how many characters were actually copied.  
      public long GetChars(int i, long fieldoffset, char[] buffer, int bufferoffset, int length) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetChars(i, fieldoffset, buffer, bufferoffset, length);  
      }  
  
      // Access the data in the specified column in the current row as a DateTime   
      public DateTime GetDateTime(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetDateTime(i);  
      }  
  
      // Access the data in the specified column in the current row as a decimal.   
      public decimal GetDecimal(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetDecimal(i);  
      }  
  
      // Access the data in the specified column in the current row as a double  
      public double GetDouble(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetDouble(i);  
      }  
  
      // Access the data in the specified column in the current row as a float  
      public float GetFloat(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetFloat(i);  
      }  
  
      // Access the data in the specified column in the current row as a Guid   
      public Guid GetGuid(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetGuid(i);  
      }  
  
      // Access the data in the specified column in the current row as a short   
      public short GetInt16(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetInt16(i);  
      }  
  
      // Access the data in the specified column in the current row as an int  
      public int GetInt32(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetInt32(i);  
      }  
  
      // Access the data in the specified column in the current row as a long   
      public long GetInt64(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetInt64(i);  
      }  
  
      // Access the data in the specified column in the current row as a string   
      public string GetString(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetString(i);  
      }  
  
      // Access the data in the specified column in the current row as an object    
      public object GetValue(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.GetValue(i);  
      }  
  
      // Returns true if and only if the data in the specified column of the current row is null as defined by the database.    
      // Note this is different than the CLR concept of null. The parameter is the column.  
      public bool IsDBNull(int i) {  
         EnsureState(StateValues.read);  
         EnsureOrdinal(i);  
         return results.IsDBNull(i);  
      }  
  
      // Utility method which executes a server side cursor motion command and reads the row at the current location of   
      // the cursor after the motion is complete.  Reading one row at a time can be inefficient, see comments at the start   
      // of this class. The parameter is the SQL cursor motion command to execute. Returns True if and only if there is data to read.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "Microsoft.Samples.SqlServer.ResultSet.EnsureState(Microsoft.Samples.SqlServer.ResultSet+StateValues,Microsoft.Samples.SqlServer.ResultSet+StateValues,System.String)")]  
      private bool fetch(string commandText) {  
         EnsureState(StateValues.read, StateValues.opened, "The result set must be open to perform the read operation.");  
         SqlCommand cmd = connection.CreateCommand();  
         cmd.CommandText = commandText;  
  
         SqlDataReader reader = null;  
         try {  
            reader = cmd.ExecuteReader();  
            // If there is no data, return false;  
            if (!reader.Read()) {  
               state = StateValues.opened;  
               return false;  
            }  
            else {  
               // Otherwise, advance the state to 'read'  
               state = StateValues.read;  
               // If we haven't cached schema information get it now  
               if (results == null) FetchMetadata(reader);  
               // Cache data values  
               object[] values = new object[FieldCount];  
               reader.GetSqlValues(values);  
               results.SetValues(values);  
               // Indicate there is data read by returning true  
               return true;  
            }  
         }  
         finally {  
            if (reader != null) {  
               reader.Close();  
               reader = null;  
            }  
         }  
      }  
  
      // Helper method for the fetch method.  Initializes the data structures which cache the schema information for the   
      // current query. The parameter is the reader from where schema information may be read.  
      private void FetchMetadata(SqlDataReader reader) {  
         int columnCount = reader.FieldCount;  
         visibleFieldCount = columnCount;  
         // Initialize the data cache  
         SqlMetaData[] metadata = new SqlMetaData[visibleFieldCount];  
  
         // Fill the schema cache for each column  
         DataTable schemaTable = reader.GetSchemaTable();  
         SqlString collationString = new SqlString(String.Empty);  
  
         for (int i = 0 ; i < metadata.Length ; i++) {  
            DataRow columnSchema = schemaTable.Rows[i];  
            metadata[i] = new SqlMetaData(  
                    reader.GetName(i),  
                    (SqlDbType)columnSchema["ProviderType"],  
                    (int)columnSchema["ColumnSize"],  
                    (byte)((short)columnSchema["NumericPrecision"]),  
                    (byte)((short)columnSchema["NumericScale"]),  
                    collationString.LCID,  
                    collationString.SqlCompareOptions,  
                    (Type)columnSchema["DataType"]  
                );  
         }  
         results = new Microsoft.SqlServer.Server.SqlDataRecord(metadata);  
      }  
  
      // Helper method which validates the state of the result set before processing a   
      // requested operation.  If the result set is in an invalid state an exception is thrown.  
      private void EnsureState(StateValues desiredState) {  
         if (state != desiredState) {  
            // Compute the default message  
            string message = string.Format(CultureInfo.InvariantCulture, "Expected result set state to be {0} but it was {1}",  
                desiredState.ToString(), state.ToString());  
            // If we have more specific information, provide a different message.  
            if (desiredState == StateValues.read)  
               message = "You must read a valid row of the result set before performing the requested operation.";  
            throw new InvalidStateException(message);  
         }  
      }  
  
      // Similar to the single argument EnsureState method except that the two specified states   
      // are both legal and a custom error message must be provided.  
      private void EnsureState(StateValues desiredState1, StateValues desiredState2, string message) {  
         if (state != desiredState1 && state != desiredState2)  
            throw new InvalidStateException(message);  
      }  
  
      // Makes certain that the requested column is valid, and throws an exception with an error message if it isn't.    
      // This would be more useful than the error message given when accessing beyond the valid boundary of an array,   
      // for example.  The parameter is the column trying to be accessed  
      private void EnsureOrdinal(int i) {  
         if (i >= results.FieldCount)  
            throw new ArgumentException(  
                string.Format(CultureInfo.InvariantCulture, "Attempt to access column {0} when only {1} columns exist",  
                i, results.FieldCount));  
      }  
  
      // Makes certain that the result set is in a proper state to read data, and that  
      // scrolling is allowed.  This method is called from methods which require scrolling capabilities.  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
      private void EnsureScroll() {  
         if (!isScrollable)  
            throw new InvalidOperationException("Attempting to execute a scroll operation on a non-scrollable result set.");  
      }  
  
      public IEnumerator GetEnumerator() {  
         return new ResultSetEnumerator(this);  
      }  
   }  
  
   public class ResultSetEnumerator : IEnumerator {  
      private bool isRead;  
  
      private ResultSet resultSetToEnumerate;  
  
      public ResultSetEnumerator(ResultSet resultSetToEnumerate) {  
         this.resultSetToEnumerate = resultSetToEnumerate;  
      }  
  
      // Returns the current element of a result set which is represented by a SqlDataRecord  
      object IEnumerator.Current {  
         get {  
            if (!isRead)  
               throw new InvalidOperationException(  
                   "The enumerator is positioned before the first element "  
                   + "of the collection or after the last element");  
            return resultSetToEnumerate.CurrentRecord;  
  
         }  
      }  
  
      [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Globalization", "CA1303:DoNotPassLiteralsAsLocalizedParameters", MessageId = "System.InvalidOperationException.#ctor(System.String)")]  
      public SqlDataRecord Current {  
         get {  
            if (!isRead)  
               throw new InvalidOperationException(  
                   "The enumerator is positioned before the first element "  
                   + "of the collection or after the last element");  
            return resultSetToEnumerate.CurrentRecord;  
         }  
      }  
  
      // Advance to the next valid element of a result set; returns True if this position has a valid element   
      public bool MoveNext() {  
         if (!isRead) {  
            if (resultSetToEnumerate.ReadFirst()) {  
               isRead = true;  
               return true;  
            }  
            else  
               return false;  
         }  
         else {  
            return resultSetToEnumerate.Read();  
         }  
      }  
  
      // Reset the current position of the enumerator to just prior to the current element  
      public void Reset() {  
         isRead = false;  
      }  
   }  
}  
```  
  
### <a name="code"></a>代码  
  
```  
// TestResultSet.cs  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Configuration;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
// Main application that increases the prices for the most popular bikes in order to demonstrate using server side cursors   
// to browser results and update in parallel.  
  
namespace Microsoft.Samples.SqlServer {  
   public sealed class TestResultSet {  
      // The factor to mulitply by the current price to get the new price for each color  
      private const String priceIncreases = "Black, 1.02, Silver, 1.01, Red, 1.05, Yellow, 1.02, Green, 1.03";  
  
      // Given the name of a color, return the price increase factor as a SqlMoney object.  
      private static readonly Dictionary<String, SqlMoney> increaseDictionary  
          = new Dictionary<String, SqlMoney>(priceIncreases.Length);  
  
      // Don't allow construction of instances since the public portion of this class is only used to contain static methods.  
      private TestResultSet() {}  
  
      // The Adventure Works Cycles corporation needs to increase the standard costs and list price for its most popular   
      // bikes due to price increases for the paint used on those bikes.  This program demonstrates browsing popular bikes   
      // and updating prices in parallel using the result set sample to implement that scenario.  Note that programmers   
      // should always consider whether using a JOIN in a server side query or update would be more efficient that using this   
      // style of programming.  
      public static void Test() {  
         // Use the priceIncreases constant to initialize entries in the increaseDictionary collection.  
         InitializeIncreaseDictionary();  
  
         SqlConnection myConnection = null;  
         bool isRSOpened = false;  
  
         // Initialize the command to get most popular bikes  
         myConnection = new SqlConnection("context connection=true");  
         ResultSet rs = null;  
         try {  
            myConnection.Open();  
            rs = new ResultSet(myConnection,  
                "SELECT TOP 10 P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice, "  
                + "sum(SOD.OrderQty) FROM Production.Product AS P "  
                + "JOIN Sales.SalesOrderDetail AS SOD ON P.ProductID = SOD.ProductID "  
                + "JOIN Production.ProductSubcategory AS PSC "  
                + "ON P.ProductSubcategoryID = PSC.ProductSubcategoryID "  
                + "JOIN Production.ProductCategory AS PC "  
                + "ON PSC.ProductCategoryID = PC.ProductCategoryID "  
                + "WHERE PC.Name = 'Bikes' "  
                + "GROUP BY P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice "  
                + "ORDER BY sum(SOD.OrderQty) desc;");  
  
            // Initialize the command to update the price of a product  
            SqlCommand updateCommand = myConnection.CreateCommand();  
            updateCommand.CommandText = "usp_UpdateProductPrice";  
            updateCommand.CommandType = CommandType.StoredProcedure;  
  
            SqlParameter productIDParameter = new SqlParameter("@ProductID", SqlDbType.Int);  
            updateCommand.Parameters.Add(productIDParameter);  
            SqlParameter standardCostParameter = new SqlParameter("@StandardCost", SqlDbType.Money);  
            updateCommand.Parameters.Add(standardCostParameter);  
            SqlParameter listPriceParameter = new SqlParameter("@ListPrice", SqlDbType.Money);  
            updateCommand.Parameters.Add(listPriceParameter);  
  
            rs.Open();  
            isRSOpened = true;  
  
            while (rs.Read()) {  
               // Column two in the result set contains the color of the bike  
               SqlMoney rateOfIncrease = increaseDictionary[rs.GetString(2)];  
  
               // Column zero in the result set contains the product ID  
               productIDParameter.Value = rs.GetInt32(0);  
  
               // Column three in the result set contains the current standard cost  
               standardCostParameter.Value = rs.GetSqlMoney(3) * rateOfIncrease;  
  
               // Column four in the result set contains the current list price  
               listPriceParameter.Value = rs.GetSqlMoney(4) * rateOfIncrease;  
  
               // Update the prices of one of the popular bikes based on its color and current prices.    
               updateCommand.ExecuteNonQuery();  
            }  
         }  
         finally {  
            if (myConnection != null) {  
  
               if (isRSOpened)  
                  rs.Close();  
  
               myConnection.Close();  
            }  
         }  
      }  
  
       // Helper function which fills the dictonary containing the price increases for each color  
      static void InitializeIncreaseDictionary() {  
         // Initialize a dictionary which contains the price increase factors for each color  
         String[] splitIncreases = priceIncreases.Split(new Char[] { ',' });  
  
         for ( int i = 0 ; i < splitIncreases.Length - 1 ; i += 2 ) {  
            increaseDictionary[splitIncreases[i].Trim()] = SqlMoney.Parse(splitIncreases[i + 1].Trim());  
         }  
      }  
   }  
}  
```  
  
### <a name="code"></a>代码  
  
```  
-- InstallCS.sql  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT [name] from sys.procedures WHERE [name] = N'usp_RSTest')  
DROP PROCEDURE usp_RSTest;  
GO  
  
IF EXISTS (SELECT [name] from sys.procedures WHERE [name] = N'usp_UpdateProductPrice')  
DROP PROCEDURE usp_UpdateProductPrice;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'TestResultSet')  
DROP ASSEMBLY TestResultSet;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'ResultSet')  
DROP ASSEMBLY ResultSet;  
GO  
  
-- Add the assembly which contains the CLR methods we want to invoke on the server.  
DECLARE @SamplesPath nvarchar(1024);  
  
CREATE ASSEMBLY [ResultSet]  
FROM 'C:\ResultSet\ResultSet.dll'  
WITH permission_set = safe;  
  
CREATE ASSEMBLY [TestResultSet]    
FROM 'C:\ResultSet\TestResultSet.dll'  
WITH permission_set = safe;  
GO  
  
CREATE PROCEDURE [usp_RSTest]  
AS EXTERNAL NAME [TestResultSet].[Microsoft.Samples.SqlServer.TestResultSet].Test  
GO  
  
CREATE PROCEDURE usp_UpdateProductPrice(  
    @ProductID int,  
    @StandardCost money,  
    @ListPrice money  
)     
AS  
SET NOCOUNT ON;  
  
UPDATE Production.Product  
SET StandardCost = @StandardCost,  
    ListPrice = @ListPrice  
WHERE ProductID = @ProductID;  
GO  
```  
  
### <a name="code"></a>代码  
  
```  
-- test.sql  
USE AdventureWorks  
GO  
  
SELECT TOP 10 P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice, sum(SOD.OrderQty) FROM Production.Product AS P  
JOIN Sales.SalesOrderDetail AS SOD ON P.ProductID = SOD.ProductID  
JOIN Production.ProductSubcategory AS PSC ON P.ProductSubcategoryID = PSC.ProductSubcategoryID  
JOIN Production.ProductCategory AS PC ON PSC.ProductCategoryID = PC.ProductCategoryID  
WHERE PC.Name = 'Bikes'  
GROUP BY P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice   
ORDER BY sum(SOD.OrderQty) desc;  
GO  
  
EXEC usp_RSTest  
GO  
  
SELECT TOP 10 P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice, sum(SOD.OrderQty) FROM Production.Product AS P  
JOIN Sales.SalesOrderDetail AS SOD ON P.ProductID = SOD.ProductID  
JOIN Production.ProductSubcategory AS PSC ON P.ProductSubcategoryID = PSC.ProductSubcategoryID  
JOIN Production.ProductCategory AS PC ON PSC.ProductCategoryID = PC.ProductCategoryID  
WHERE PC.Name = 'Bikes'  
GROUP BY P.ProductID, P.Name, P.Color, P.StandardCost, P.ListPrice   
ORDER BY sum(SOD.OrderQty) desc;  
GO  
  
```  
  
### <a name="code"></a>代码  
  
```  
-- Cleanup.sql  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT [name] from sys.procedures WHERE [name] = N'usp_RSTest')  
DROP PROCEDURE usp_RSTest;  
GO  
  
IF EXISTS (SELECT [name] from sys.procedures WHERE [name] = N'usp_UpdateProductPrice')  
DROP PROCEDURE usp_UpdateProductPrice;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'TestResultSet')  
DROP ASSEMBLY TestResultSet;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'ResultSet')  
DROP ASSEMBLY ResultSet;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
