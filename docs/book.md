
# C#：从入门到精通（.NET 8 实战版）

## 目录
- [第 1 章 初识 C# 与 .NET](#第-1-章-初识-c-与-net)
- [第 2 章 类型系统总览](#第-2-章-类型系统总览)
- [第 3 章 变量与表达式](#第-3-章-变量与表达式)
- [第 4 章 流程控制](#第-4-章-流程控制)
- [第 5 章 方法与参数](#第-5-章-方法与参数)
- [第 6 章 类 class 与对象](#第-6-章-类-class-与对象)
- [第 7 章 结构体 struct 与只读结构体](#第-7-章-结构体-struct-与只读结构体)
- [第 8 章 枚举 enum 与标志枚举](#第-8-章-枚举-enum-与标志枚举)
- [第 9 章 继承与多态](#第-9-章-继承与多态)
- [第 10 章 接口 interface 与显式接口实现](#第-10-章-接口-interface-与显式接口实现)
- [第 11 章 属性 property 与索引器](#第-11-章-属性-property-与索引器)
- [第 12 章 运算符重载与相等性](#第-12-章-运算符重载与相等性)
- [第 13 章 命名空间与程序集](#第-13-章-命名空间与程序集)
- [第 14 章 特性 Attribute 与元数据](#第-14-章-特性-attribute-与元数据)
- [第 15 章 预处理指令](#第-15-章-预处理指令)
- [第 16 章 正则表达式 Regex](#第-16-章-正则表达式-regex)
- [第 17 章 委托与 Lambda](#第-17-章-委托与-lambda)
- [第 18 章 事件 event 模式](#第-18-章-事件-event-模式)
- [第 19 章 泛型](#第-19-章-泛型)
- [第 20 章 集合](#第-20-章-集合)
- [第 21 章 LINQ](#第-21-章-linq)
- [第 22 章 异常处理](#第-22-章-异常处理)
- [第 23 章 日志与调试](#第-23-章-日志与调试)
- [第 24 章 任务并行库 TPL](#第-24-章-任务并行库-tpl)
- [第 25 章 并发模型](#第-25-章-并发模型)
- [第 26 章 异步流](#第-26-章-异步流)
- [第 27 章 反射与发射](#第-27-章-反射与发射)
- [第 28 章 源生成器与 Roslyn 分析器](#第-28-章-源生成器与-roslyn-分析器)
- [第 29 章 内存管理](#第-29-章-内存管理)
- [第 30 章 高性能 C#](#第-30-章-高性能-c)
- [第 31 章 基准测试](#第-31-章-基准测试)
- [第 32 章 文件与流](#第-32-章-文件与流)
- [第 33 章 序列化](#第-33-章-序列化)
- [第 34 章 网络](#第-34-章-网络)
- [第 35 章 ASP.NET Core 最小 API / MVC](#第-35-章-aspnet-core-最小-api--mvc)
- [第 36 章 数据访问](#第-36-章-数据访问)
- [第 37 章 不安全代码](#第-37-章-不安全代码)
- [第 38 章 PInvoke 与互操作](#第-38-章-pinvoke-与互操作)
- [第 39 章 解决方案结构与包管理](#第-39-章-解决方案结构与包管理)
- [第 40 章 测试与质量](#第-40-章-测试与质量)
- [第 41 章 构建与发布](#第-41-章-构建与发布)
- [第 42 章 实战 A：命令行日志分析器](#第-42-章-实战-a命令行日志分析器)
- [第 43 章 实战 B：待办清单 API](#第-43-章-实战-b待办清单-api)
- [第 44 章 实战 C：高并发 URL 短链服务](#第-44-章-实战-c高并发-url-短链服务)
- [附录 A 术语表](#附录-a-术语表)
- [附录 B 常见错误与调试清单](#附录-b-常见错误与调试清单)
- [附录 C 关键 API 速查表](#附录-c-关键-api-速查表)
- [附录 D 面试题与参考答案](#附录-d-面试题与参考答案)
- [附录 E 进一步学习资源](#附录-e-进一步学习资源)


## 第 1 章 初识 C# 与 .NET

### 本章目标
- 理解公共语言运行时（CLR）与通用类型系统（CTS）的角色。
- 熟悉 .NET 8 项目的目录结构与 `dotnet` CLI 工作流。
- 编写第一个 "Hello World" 控制台程序并了解编译执行流程。
- 区分 JIT、AOT 与基础类库（BCL）的作用场景。

### 关键术语
- 公共语言运行时 *Common Language Runtime, CLR*：托管代码执行引擎，负责内存管理、安全与异常。
- 通用类型系统 *Common Type System, CTS*：定义所有 .NET 语言共享的类型与行为规范。
- 公共语言规范 *Common Language Specification, CLS*：语言互操作所需的最小特性子集。
- 即时编译 *Just-In-Time compilation, JIT*：运行时按需将 IL 转换为机器码。
- 预先编译 *Ahead-Of-Time compilation, AOT*：在部署前生成机器码，减少启动成本。

### 核心概念与原理
- .NET 8 提供跨平台的 CLR，C# 源码经由 Roslyn 编译器生成中间语言 *Intermediate Language, IL*，由 JIT 或 NativeAOT 编译器生成机器码。
- CTS 确保所有语言共享一致的类型系统，CLS 是 CTS 的可互操作子集。不同语言可以共享程序集 *assembly*。
- 项目结构通常包含 `src/`、`tests/` 与 `samples/`。解决方案 `.sln` 管理多个项目 `.csproj`。`dotnet build` 负责还原依赖、编译并输出到 `bin/`。
- BCL 提供 `System.*` 命名空间下的核心 API，如 `System.Console`、`System.Collections`。了解 BCL 有助于不重复造轮子。

ASCII 图：
```
C# 源码 --(Roslyn 编译)--> IL + 元数据 --(JIT/AOT)--> 机器码
                   |                              |
                 CTS/CLS ------------------------> 托管执行环境
```

### 最小可运行示例
```bash
mkdir -p src/Chapter01.HelloWorld
cd src/Chapter01.HelloWorld
dotnet new console -n Chapter01.HelloWorld -f net8.0
```

`Program.cs`：
```csharp
using System;

Console.WriteLine("Hello, .NET 8!");
Console.WriteLine($"当前运行时: {Environment.Version}");
```

### 进阶示例
#### 示例 1：探索编译输出
```bash
dotnet build
ls bin/Debug/net8.0
```
正确：查看 `Chapter01.HelloWorld.dll` 与 `.deps.json`。

#### 示例 2：使用 AOT 发布
```bash
dotnet publish -c Release -r win-x64 --self-contained true /p:PublishAot=true
```
说明：AOT 生成单文件可执行，缩短启动时间，适用于容器与 CLI 工具。

### 最佳实践
- 始终使用最新稳定 SDK（通过 `global.json` 锁定版本）。
- 组织解决方案目录，区分生产代码与测试、样例。
- 利用 `dotnet --info` 检查环境，确保跨平台一致性。
- 把构建、发布命令写入 `README` 或脚本，保证团队共享流程。

### 常见陷阱
1. **项目未初始化 Git**：
```bash
# 错误：直接修改无版本控制
```
修正：`git init` 并提交。
2. **混用旧版 SDK**：
```bash
dotnet new console -f net6.0
```
修正：统一 `net8.0`，旧项目需升级依赖。
3. **忽略 `dotnet restore`**：
首次构建失败，提示缺少包。修正：运行 `dotnet restore` 或 `dotnet build` 自动执行。

### 练习
1. 判断题：.NET 运行时负责垃圾回收？
2. 简答：JIT 与 AOT 的差异是什么？
3. 操作：创建名为 `IntroDemo` 的控制台项目并输出当前时间。
4. 思考：为何 CTS 对跨语言协作重要？
5. 编程：修改示例，读取命令行参数并打印首个参数。

**参考答案**
1. 是。
2. JIT 在运行时编译 IL，AOT 在发布阶段生成机器码，权衡启动速度与灵活性。
3. 使用 `dotnet new console -n IntroDemo -f net8.0`，`Console.WriteLine(DateTime.Now);`。
4. CTS 定义统一类型语义，避免语言边界出现隐式转换错误。
5. 通过 `Console.WriteLine(args.Length > 0 ? args[0] : "未提供参数");`。

### 小结
- C# 编译产物是 IL，由 CLR 管理执行生命周期。
- 熟悉 `dotnet` CLI 与解决方案结构是团队协作的第一步。
- JIT 与 AOT 提供灵活部署策略。
- BCL 是日常开发的基础库，应优先查阅官方 API。

### 参考链接/文档关键词
- ".NET Fundamentals"
- "dotnet CLI overview"
- "CLR vs CoreCLR"
- "Publish AOT .NET 8"


## 第 2 章 类型系统总览

### 本章目标
- 区分值类型 *value type* 与引用类型 *reference type* 的内存语义。
- 理解装箱 *boxing*、拆箱 *unboxing* 与性能影响。
- 掌握 `null`、可空值类型 `Nullable<T>` 与可空引用类型注解。
- 认识 `string` 的不可变性与驻留 *interning*。

### 关键术语
- 值类型 *value type*：在栈或嵌入位置直接存储数据，如 `int`、`struct`。
- 引用类型 *reference type*：在托管堆上存储对象，通过引用访问，如 `class`、`string`。
- 装箱 *boxing*：将值类型复制到堆中，包装为 `object`。
- 拆箱 *unboxing*：从 `object` 提取原始值类型，需要类型匹配。
- 可空性 *nullability*：编译器通过注解分析潜在的 `null` 引用错误。

### 核心概念与原理
- 值类型默认按值复制，生命周期通常随作用域结束；引用类型复制的是托管堆地址。GC 负责释放未引用的对象。
- 装箱会在堆上创建新对象，拆箱需要显式转换且可能引发 `InvalidCastException`。泛型可避免装箱。
- `Nullable<T>` 为值类型引入三态逻辑（有值/无值），C# 8 引入可空引用类型，通过 `?` 与注解分析潜在 `NullReferenceException`。
- `string` 为引用类型但不可变 *immutable*。驻留机制在编译期与运行时缓存相同字符串，降低重复分配。

ASCII 表：
| 类型类别 | 存储位置 | 示例 | 装箱成本 |
| --- | --- | --- | --- |
| 值类型 | 栈/嵌入 | `int`, `bool`, `struct` | 高 |
| 引用类型 | 堆 | `class`, `string`, `array` | 无 |

### 最小可运行示例
```bash
mkdir -p src/Chapter02.TypeSystem
cd src/Chapter02.TypeSystem
dotnet new console -n Chapter02.TypeSystem -f net8.0
```

`Program.cs`：
```csharp
using System;

int number = 42; // 值类型
object boxed = number; // 装箱
int unboxed = (int)boxed; // 拆箱
string text = "dotnet";
Console.WriteLine($"number={number}, boxed={boxed}, unboxed={unboxed}, text length={text.Length}");
```

### 进阶示例
#### 示例 1：避免装箱的泛型集合
```csharp
using System.Collections.Generic;

List<int> numbers = new() { 1, 2, 3 };
foreach (int value in numbers)
{
    Console.WriteLine(value);
}
```
对比错误写法：
```csharp
ArrayList list = new() { 1, 2, 3 }; // System.Collections，值类型被装箱
```

#### 示例 2：可空引用类型警告
```csharp
string? maybeName = Console.ReadLine();
if (!string.IsNullOrWhiteSpace(maybeName))
{
    Console.WriteLine(maybeName.ToUpperInvariant());
}
```
错误写法：
```csharp
string? maybeName = null;
Console.WriteLine(maybeName.ToUpper()); // 编译器警告 + 运行时异常
```

### 最佳实践
- 针对数值集合优先使用泛型集合，避免装箱成本。
- 启用可空引用类型（`<Nullable>enable</Nullable>`），配合 `!` 抑制符谨慎使用。
- 利用 `string.Create` 或插值降低临时字符串数量。
- 结构体应保持小而不可变，避免频繁复制。

### 常见陷阱
1. **值类型默认构造**：
```csharp
DateTime date = new(); // 值为 DateTime.MinValue，不是 null
```
修正：明确初始化。
2. **拆箱类型不匹配**：
```csharp
object boxed = 42;
short value = (short)boxed; // InvalidCastException
```
修正：先转换为 `int` 后再显式转换。
3. **误认为字符串可变**：
```csharp
string s = "abc";
s[0] = 'z'; // 编译错误
```
修正：使用 `StringBuilder` 或重新创建新字符串。

### 练习
1. 判断：结构体可以被赋值为 `null` 吗？
2. 简答：装箱发生时的内存流程是什么？
3. 编程：声明 `Span<int>` 并从数组切片。
4. 思考：为什么 `string` 设计为不可变？
5. 改错：修复代码 `object obj = 1; byte b = (byte)obj;`。

**参考答案**
1. 否，除非使用 `Nullable<T>`。
2. 值类型复制到托管堆，分配新对象并把值封装为 `object` 引用。
3. `int[] data = {1,2,3}; Span<int> span = data.AsSpan(1,2);`。
4. 不可变可提高线程安全、驻留效率并支持字面量共享。
5. 先拆箱为 `int value = (int)obj; byte b = (byte)value;`。

### 小结
- 理解值/引用类型有助于编写高性能代码。
- 可空性分析在编译期减少空引用风险。
- 装箱/拆箱是性能隐患，泛型是首选解决方案。
- 字符串不可变且驻留，适合缓存但需注意拼接成本。

### 参考链接/文档关键词
- "Value types vs Reference types"
- "Nullable reference types"
- "Boxing and Unboxing"
- "String interning"


## 第 3 章 变量与表达式

### 本章目标
- 理解变量生命周期、作用域与命名规范。
- 熟悉字面量、类型推断 `var` 的适用场景。
- 掌握算术、逻辑、位运算符及优先级。
- 学会使用 `checked`/`unchecked` 控制溢出。

### 关键术语
- 变量 *variable*：在执行期间保存数据的命名存储位置。
- 字面量 *literal*：源代码中直接写出的常量值，如 `42`、`"text"`。
- 类型推断 *type inference*：编译器根据右侧表达式推断类型。
- 溢出检查 *checked context*：检测数值运算超出范围并抛出异常。

### 核心概念与原理
- 变量作用域遵循块级 `{}`，局部变量必须先赋值再使用；`const` 在编译期替换字面量。
- `var` 仅在右值类型显而易见时使用，保持可读性。匿名类型必须使用 `var`。
- 运算符遵循优先级与结合性，合理使用括号避免歧义。C# 支持前后缀自增、空合并 `??`、三元运算符 `?:`。
- `checked` 块可捕获溢出，例如 `int.MaxValue + 1`。默认上下文受项目 `CheckForOverflowUnderflow` 影响。

### 最小可运行示例
```bash
mkdir -p src/Chapter03.Expressions
cd src/Chapter03.Expressions
dotnet new console -n Chapter03.Expressions -f net8.0
```

`Program.cs`：
```csharp
int a = 10;
int b = 20;
int sum = a + b;
int uncheckedResult = unchecked(int.MaxValue + 1);
int checkedResult;
try
{
    checkedResult = checked(int.MaxValue + 1);
}
catch (OverflowException ex)
{
    Console.WriteLine($"捕获溢出: {ex.Message}");
    checkedResult = int.MaxValue;
}
Console.WriteLine($"sum={sum}, unchecked={uncheckedResult}, checked={checkedResult}");
```

### 进阶示例
#### 示例 1：`var` 的正确与错误使用
```csharp
var count = GetOrderCount(); // 正确：方法返回类型显而易见
int explicitCount = GetOrderCount(); // 同样可读

var query = new { Id = 1, Name = "Demo" }; // 匿名类型必须使用 var
```
错误：
```csharp
var result = DoSomethingUnknown(); // 类型不明显，阅读困难
```

#### 示例 2：运算符优先级
```csharp
int priority = 2 + 3 * 4; // 14
int grouped = (2 + 3) * 4; // 20
bool logic = true || false && false; // true -> && 优先级高
```
错误：
```csharp
bool trap = (true || false) && false; // false，与预期不符
```

### 最佳实践
- 变量命名遵循 camelCase，避免缩写。
- `var` 仅在表达式类型明显或匿名类型时使用。
- 使用 `const` 与 `readonly` 表达不变意图。
- 通过单元测试覆盖关键表达式与边界情况。

### 常见陷阱
1. **未初始化变量**：
```csharp
int value;
Console.WriteLine(value); // 编译错误 CS0165
```
修正：先赋值。
2. **浮点比较**：
```csharp
double x = 0.1 + 0.2;
if (x == 0.3) { } // 可能为 false
```
修正：使用误差范围 `Math.Abs(x - 0.3) < 1e-6`。
3. **整数除法截断**：
```csharp
int avg = 5 / 2; // 结果 2
```
修正：显式转换 `double avg = 5 / 2.0;`。

### 练习
1. 判断：`var` 声明的变量在编译后是 `dynamic` 吗？
2. 简答：`checked` 与 `unchecked` 的差异。
3. 编程：使用位运算实现简单掩码 `0b1010 & 0b1100`。
4. 思考：何时需要使用 `readonly struct` 控制复制？（预告第 7 章）
5. 改错：`int result = 10 / (a + b);` 当 `a=-b` 时发生什么？如何防御？

**参考答案**
1. 否，`var` 仍为静态类型推断。
2. `checked` 检测溢出并抛异常，`unchecked` 忽略溢出。
3. 结果为 `0b1000` 或十进制 8。
4. 当结构体较大且需避免复制时，使用 `in` 参数与 `readonly struct`。
5. `DivideByZeroException`，应在计算前验证分母不为零。

### 小结
- 变量生命周期与作用域是理解内存的基础。
- 运算符优先级需谨慎使用括号避免逻辑错误。
- `checked`/`unchecked` 提供数值安全控制。
- 选择合适的类型推断平衡可读性与精确性。

### 参考链接/文档关键词
- "C# variables scope"
- "checked keyword"
- "C# operators precedence"
- "var keyword guidelines"

## 第 4 章 流程控制

### 本章目标
- 掌握 `if/else`、`switch` 与模式匹配 *pattern matching* 的常用写法。
- 熟悉 `for`、`while`、`do/while`、`foreach` 循环的适用场景。
- 了解 `break`、`continue`、`return` 的语义。
- 学习 `goto` 的替代方案，如方法拆分与状态机。

### 关键术语
- 条件语句 *conditional statement*：根据布尔表达式选择执行路径。
- 模式匹配 *pattern matching*：将对象与模式匹配以提取值或判断类型。
- 循环 *loop*：重复执行代码块的结构。
- 状态机 *state machine*：显式维护状态转移的代码结构。

### 核心概念与原理
- `if/else` 根据布尔条件执行分支，`switch` 在 C# 8 之后支持表达式、模式与守卫。模式匹配支持类型、常量、关系、属性模式。
- 循环语句需谨慎控制终止条件，避免无限循环。`foreach` 遍历实现了 `IEnumerable` 的集合。
- `goto` 会降低可读性，现代 C# 使用方法提取、`switch` 表达式或状态枚举替代。

### 最小可运行示例
```bash
mkdir -p src/Chapter04.ControlFlow
cd src/Chapter04.ControlFlow
dotnet new console -n Chapter04.ControlFlow -f net8.0
```

`Program.cs`：
```csharp
int score = int.Parse(args.Length > 0 ? args[0] : "85");
string grade = score switch
{
    >= 90 => "优秀",
    >= 80 => "良好",
    >= 60 => "及格",
    _ => "不及格"
};
Console.WriteLine($"score={score}, grade={grade}");
```

### 进阶示例
#### 示例 1：属性模式
```csharp
bool IsVip(Customer customer) => customer switch
{
    { IsActive: true, Level: >= CustomerLevel.Gold } => true,
    _ => false
};
```
错误：使用 `if (customer.Level == CustomerLevel.Gold && customer.IsActive == true)` 嵌套多层分支，难以阅读。

#### 示例 2：循环与取消
```csharp
CancellationTokenSource cts = new(TimeSpan.FromSeconds(5));
int i = 0;
while (!cts.IsCancellationRequested && i < 100)
{
    Console.WriteLine(i++);
    await Task.Delay(100, cts.Token);
}
```
错误：未处理取消导致 `TaskCanceledException` 泄漏。

### 最佳实践
- 将复杂条件拆分为具名布尔变量或方法。
- 使用模式匹配表达领域规则，避免魔法数字。
- 循环中及时释放资源，`foreach` 自动调用 `Dispose`。
- 对长循环引入 `CancellationToken` 与超时。

### 常见陷阱
1. **漏掉 `default` 分支**：
```csharp
switch (status)
{
    case OrderStatus.New: break;
    case OrderStatus.Paid: break;
}
```
修正：添加 `_ =>` 或显式处理所有枚举值。
2. **`switch` 穿透误解**：C# 不允许自动贯穿，应使用 `goto case` 或多个模式。
3. **无限循环**：
```csharp
while (true) { } // CPU 100%
```
修正：增加 `break` 条件或 `await Task.Delay`。

### 练习
1. 判断：`switch` 表达式是否必须涵盖所有可能？
2. 简答：如何利用关系模式简化分支？
3. 编程：用 `foreach` 遍历 `Dictionary` 并打印键值。
4. 思考：什么时候选择状态机而非多层 `if/else`？
5. 改错：`for (int i=0; i<=list.Count; i++)` 有何问题？

**参考答案**
1. 是，否则编译错误或需 `_` 兜底。
2. 直接在模式中写比较，如 `score is >= 90 and <= 100`。
3. `foreach (var (key, value) in dictionary) Console.WriteLine($"{key}:{value}");`
4. 当状态转移复杂、需事件驱动时使用状态模式。
5. 越界访问，终止条件应为 `< list.Count`。

### 小结
- 条件与循环构成程序流程骨架。
- 模式匹配让分支表达式更声明式。
- 控制流需搭配取消、异常处理保障健壮性。

### 参考链接/文档关键词
- "C# switch expression"
- "Pattern matching"
- "C# loops"
- "Finite state machine design"

## 第 5 章 方法与参数

### 本章目标
- 理解方法签名、返回值与重载。
- 熟悉 `ref`、`out`、`in` 参数差异。
- 学会使用命名参数与可选参数。
- 掌握局部函数与迭代器 `yield` 的应用。

### 关键术语
- 方法 *method*：封装可复用逻辑的成员。
- 参数修饰符 *parameter modifier*：`ref`（引用传递）、`out`（输出）、`in`（只读引用）。
- 局部函数 *local function*：定义在方法内部的函数。
- 迭代器 *iterator*：使用 `yield return`/`yield break` 延迟生成序列。

### 核心概念与原理
- 方法签名由名称、参数列表（含修饰符、泛型约束）组成。返回类型不参与重载。
- `ref` 需要调用前初始化；`out` 在方法内赋值；`in` 传递只读引用避免大结构复制。
- 命名参数提高可读性，顺序可调整但命名后续参数必须继续命名。
- 迭代器编译为状态机，支持延迟执行与 `foreach`。

### 最小可运行示例
```bash
mkdir -p src/Chapter05.Methods
cd src/Chapter05.Methods
dotnet new console -n Chapter05.Methods -f net8.0
```

`Program.cs`：
```csharp
static int Sum(ReadOnlySpan<int> values)
{
    int total = 0;
    foreach (int value in values)
    {
        total += value;
    }
    return total;
}

int[] data = { 1, 2, 3 };
Console.WriteLine(Sum(data));
```

### 进阶示例
#### 示例 1：`ref` 与 `out`
```csharp
static void Update(ref int target, out int doubled)
{
    target += 10;
    doubled = target * 2;
}

int value = 5;
Update(ref value, out int result);
Console.WriteLine($"value={value}, result={result}");
```
错误：未赋值 `out` 参数会导致编译错误。

#### 示例 2：迭代器生成 Fibonacci
```csharp
static IEnumerable<int> GenerateFibonacci(int count)
{
    int current = 0, next = 1;
    for (int i = 0; i < count; i++)
    {
        yield return current;
        (current, next) = (next, current + next);
    }
}

foreach (int value in GenerateFibonacci(5))
{
    Console.WriteLine(value);
}
```

### 最佳实践
- 优先使用表达式明确的参数名称，避免过多布尔参数。
- 对大结构体使用 `in` 参数或 `ReadOnlySpan<T>` 以减少复制。
- 迭代器方法内部避免 `try/finally` 开销，必要时使用 `await foreach`。
- 在公共 API 上提供文档注释 `///`，配合 XML doc。

### 常见陷阱
1. **`ref` 忘记初始化**：调用前必须赋值。
2. **可选参数位置变化**：改变默认值顺序会破坏二进制兼容性。
3. **迭代器异常处理**：`yield` 过程中抛出的异常在枚举时才触发，应记录日志。

### 练习
1. 判断：方法返回类型能区分重载吗？
2. 简答：`ref readonly` 的作用。
3. 编程：实现 `IEnumerable<int>` 的扩展方法 `SumPositive()`。
4. 思考：何时使用局部函数代替私有方法？
5. 改错：`yield return` 写在 `try` 块中需要注意什么？

**参考答案**
1. 否。
2. 向调用方提供只读引用以减少复制。
3. 遍历集合并累加大于零的数。
4. 当逻辑仅被单个方法使用且需要捕获局部变量。
5. `try/finally` 会影响状态机性能，避免在 `catch` 中 `yield`。

### 小结
- 参数修饰符控制传递语义，是性能优化常用手段。
- 可选参数与命名参数提升 API 友好性。
- 迭代器与局部函数帮助拆分复杂逻辑。

### 参考链接/文档关键词
- "C# ref out in"
- "Optional parameters"
- "Iterators yield"
- "Local functions"

## 第 6 章 类 class 与对象

### 本章目标
- 理解封装、构造函数、析构函数的职责。
- 掌握静态成员、实例成员与访问修饰符。
- 熟悉 `record` 类型与 C# 12 主构造函数 *primary constructor*。
- 了解对象初始化器、不可变对象设计。

### 关键术语
- 封装 *encapsulation*：隐藏实现细节，暴露稳定接口。
- 构造函数 *constructor*：初始化对象状态的特殊方法。
- 析构函数 *finalizer*：在垃圾回收时清理非托管资源。
- 记录类型 *record*：用于不可变数据承载，内建值相等语义。

### 核心概念与原理
- 类在托管堆分配，构造函数执行后才能使用。析构函数在 GC 第一次回收后执行，需谨慎避免阻塞。
- 静态成员绑定到类型本身，常用于共享资源或工厂模式。
- C# 12 主构造函数允许在类型声明处定义参数并映射到属性，简化注入。
- `record` 默认提供值相等、`with` 表达式，适合 DTO 或配置模型。

### 最小可运行示例
```bash
mkdir -p src/Chapter06.Classes
cd src/Chapter06.Classes
dotnet new console -n Chapter06.Classes -f net8.0
```

`Program.cs`：
```csharp
namespace Book.Samples.Chapter06;

public class Greeter(string message)
{
    public string Message { get; } = message;
    public void SayHello() => Console.WriteLine(Message);
}

Greeter greeter = new("Hello from class!");
greeter.SayHello();
```

### 进阶示例
#### 示例 1：`record` 与不可变对象
```csharp
public record Customer(string Id, string Name)
{
    public string Email { get; init; } = string.Empty;
}

Customer alice = new("001", "Alice") { Email = "alice@example.com" };
Customer renamed = alice with { Name = "Alice Chen" };
Console.WriteLine(renamed);
```

#### 示例 2：资源释放模式
```csharp
public sealed class FileWriter : IDisposable
{
    private readonly StreamWriter writer;
    public FileWriter(string path) => writer = new(path);
    public void WriteLine(string text) => writer.WriteLine(text);
    public void Dispose()
    {
        writer.Dispose();
        GC.SuppressFinalize(this);
    }
}

using FileWriter writer = new("output.log");
writer.WriteLine("hello");
```
错误：遗漏 `Dispose()` 导致文件句柄泄漏。

### 最佳实践
- 通过构造函数注入依赖，避免服务定位器。
- 在公共类上编写 XML 注释，生成文档。
- 资源类实现 `IDisposable`，并提供 `Dispose(bool)` 模式。
- 使用 `sealed` 优化虚表调用（除非需要继承）。

### 常见陷阱
1. **在构造函数中调用虚方法**：可能调用到未初始化子类。
2. **忘记抑制终结器**：`GC.SuppressFinalize` 可减少 GC 成本。
3. **误用 `record class`**：值相等语义可能导致集合键重复，应重写 `GetHashCode` 或使用 `record struct`。

### 练习
1. 判断：`record` 默认是引用类型吗？
2. 简答：主构造函数与传统构造函数的关系。
3. 编程：实现 `Lazy<T>` 风格的延迟加载属性。
4. 思考：封装与信息隐藏对模块化的意义。
5. 改错：`public class Foo { ~Foo() { Dispose(); } }` 有何风险？

**参考答案**
1. 是，除非声明为 `record struct`。
2. 主构造函数在类型主体内可访问参数，仍可定义其他构造函数。
3. 使用私有字段与空合并运算符实现。
4. 封装减少耦合，提高可维护性与测试性。
5. 在终结器中调用可能访问已释放资源且抛出异常，应仅处理非托管句柄。

### 小结
- 类提供面向对象封装能力，与记录类型协同表达数据模型。
- 主构造函数简化依赖注入与不可变对象创建。
- 资源释放需遵循 `IDisposable` 模式。

### 参考链接/文档关键词
- "C# primary constructor"
- "record types"
- "IDisposable pattern"
- "Class vs struct"


## 第 7 章 结构体 struct 与只读结构体

### 本章目标
- 区分类与结构体的内存布局与适用场景。
- 使用 `struct`、`readonly struct` 与 C# 12 主构造函数。
- 了解 `with` 在结构体上的行为及版本差异。
- 理解可变结构体带来的潜在副作用。

### 关键术语
- 结构体 *struct*：值类型，适合小型数据载体。
- 只读结构体 *readonly struct*：保证字段不可变，避免隐式复制。
- 可变结构体 *mutable struct*：允许修改，但易导致状态不一致。
- 结构体复制 *struct copy*：赋值或传参时按值复制。

### 核心概念与原理
- 结构体在栈或嵌入字段中分配，避免 GC 压力。可用于高频调用的点坐标、颜色等。
- `readonly struct` 与 `ref readonly` 搭配可避免复制并防止修改。C# 12 支持主构造函数简化初始化。
- `with` 在 `record struct` 中可用，在普通 `struct` 自 C# 10 起支持 `with` 表达式创建副本。

### 最小可运行示例
```bash
mkdir -p src/Chapter07.Structs
cd src/Chapter07.Structs
dotnet new console -n Chapter07.Structs -f net8.0
```

`Program.cs`：
```csharp
namespace Book.Samples.Chapter07;

public readonly struct Point(double x, double y)
{
    public double X { get; } = x;
    public double Y { get; } = y;
    public double Length => Math.Sqrt(X * X + Y * Y);
}

Point p = new(3, 4);
Console.WriteLine(p.Length);
```

### 进阶示例
#### 示例 1：可变结构体的陷阱
```csharp
public struct Counter
{
    public int Value { get; private set; }
    public void Increment() => Value++;
}

Counter counter = new();
List<Counter> list = new() { counter };
list[0].Increment(); // 无效，值复制
```
修正：使用 `class` 或 `ref` 返回。

#### 示例 2：`with` 表达式
```csharp
public struct Size(int width, int height)
{
    public int Width { get; } = width;
    public int Height { get; } = height;
}

Size original = new(100, 50);
Size scaled = original with { Width = 200 };
Console.WriteLine(scaled.Width);
```

### 最佳实践
- 结构体大小保持在 16 字节左右，避免包含引用类型字段。
- 使用 `readonly struct`、`init` 属性表达不可变性。
- 对性能敏感场景使用 `in` 参数与 `ref` 返回。

### 常见陷阱
1. **结构体默认构造**：字段初始化为默认值，需确保逻辑正确。
2. **在属性 getter 中返回可修改结构体**：可能被复制修改。
3. **箱化结构体**：`object` 调用导致装箱，应实现 `IEquatable<T>`。

### 练习
1. 判断：结构体可继承自其他结构体吗？
2. 简答：`readonly struct` 的优势。
3. 编程：定义 `readonly struct Rectangle(double width, double height)`，提供 `Area` 属性。
4. 思考：何时需要使用 `ref struct`（预告第 30 章）。
5. 改错：解释为何 `list[0].Increment();` 无效。

**参考答案**
1. 否，只能实现接口。
2. 避免隐式复制并提升线程安全。
3. `public double Area => width * height;`。
4. 当类型包含 `Span<T>` 等栈限定成员。
5. `list[0]` 返回副本，修改不影响原始元素。

### 小结
- 结构体适用于轻量数据，`readonly` 保障不可变。
- `with` 表达式让复制修改更安全。
- 避免可变结构体导致状态错位。

### 参考链接/文档关键词
- "C# struct guidelines"
- "readonly struct"
- "with expression"
- "Mutable structs"

## 第 8 章 枚举 enum 与标志枚举

### 本章目标
- 掌握枚举 *enum* 定义与基础使用。
- 理解 `[Flags]` 标志枚举的位运算语义。
- 了解底层基类型、自定义起始值。
- 学会使用 `Enum.HasFlag`、`Enum.TryParse`。

### 关键术语
- 枚举 *enumeration*：命名的常量集合。
- 标志枚举 *flags enum*：每个成员代表一个位标志，可组合。
- 基底类型 *underlying type*：`enum` 默认为 `int`，可指定 `byte` 等。
- 位掩码 *bitmask*：通过位运算组合和检查标志。

### 核心概念与原理
- 枚举提高可读性并限制取值范围。底层仍是数值，可与数据库或配置映射。
- `[Flags]` 枚举成员值应为 2 的幂，`0` 代表无标志。组合使用 `|`，检测使用 `HasFlag` 或 `(value & flag) != 0`。
- 使用 `Enum.TryParse` 支持从字符串转换并忽略大小写。

### 最小可运行示例
```bash
mkdir -p src/Chapter08.Enums
cd src/Chapter08.Enums
dotnet new console -n Chapter08.Enums -f net8.0
```

`Program.cs`：
```csharp
[Flags]
public enum Permission
{
    None = 0,
    Read = 1 << 0,
    Write = 1 << 1,
    Execute = 1 << 2
}

Permission user = Permission.Read | Permission.Write;
Console.WriteLine(user);
Console.WriteLine(user.HasFlag(Permission.Execute));
```

### 进阶示例
#### 示例 1：解析字符串
```csharp
if (Enum.TryParse<Permission>("Read, Execute", ignoreCase: true, out var flags))
{
    Console.WriteLine(flags);
}
```
错误：`Enum.Parse` 未捕获异常。

#### 示例 2：自定义基类型
```csharp
public enum Status : byte
{
    New = 1,
    Completed = 2,
    Archived = 3
}
Console.WriteLine((byte)Status.Completed);
```

### 最佳实践
- 对外暴露的标志枚举提供组合常量，如 `ReadWrite`。
- 在数据库中存储枚举时使用整数或字符串保持可读性。
- 使用 `Enum.IsDefined` 验证输入。

### 常见陷阱
1. **未设置 `[Flags]`**：组合输出显示数字。
2. **使用非幂值**：导致组合重复或冲突。
3. **序列化大小写不一致**：使用 `JsonStringEnumConverter` 保持可读。

### 练习
1. 判断：枚举可继承？
2. 简答：为何标志枚举的默认值应为 0？
3. 编程：实现 `PermissionExtensions.HasAll()` 扩展方法。
4. 思考：何时避免使用 `HasFlag`？
5. 改错：`Permission.Read | Permission.Write | Permission.Read`。

**参考答案**
1. 否。
2. 表示无标志且易于清除状态。
3. 使用 `(value & required) == required`。
4. 在高性能场景使用位运算比较快。
5. 重复标志可省略，或使用组合常量。

### 小结
- 枚举让代码语义明确，标志枚举表示组合状态。
- 合理设置基底类型有助于压缩存储。
- 转换和验证避免输入非法值。

### 参考链接/文档关键词
- "C# enum flags"
- "Enum.TryParse"
- "JsonStringEnumConverter"
- "Enum best practices"

## 第 9 章 继承与多态

### 本章目标
- 理解继承层次、基类/派生类关系。
- 掌握虚方法、抽象类、密封类的使用。
- 了解 `new` 隐藏与里氏替换原则。
- 设计可测试、可扩展的继承层次。

### 关键术语
- 基类 *base class*：提供公共行为的父类型。
- 虚方法 *virtual method*：允许子类重写的成员。
- 抽象类 *abstract class*：不能实例化，定义模板。
- 里氏替换原则 *Liskov Substitution Principle*：子类可替代基类。

### 核心概念与原理
- 继承提供行为共享，但过深层次增加耦合。优先组合。
- 虚方法与抽象方法区别：虚方法有默认实现，抽象方法必须重写。
- `sealed` 防止进一步继承。`new` 关键字隐藏同名成员，但破坏多态。

### 最小可运行示例
```bash
mkdir -p src/Chapter09.Inheritance
cd src/Chapter09.Inheritance
dotnet new console -n Chapter09.Inheritance -f net8.0
```

`Program.cs`：
```csharp
public abstract class Shape
{
    public abstract double Area();
}

public sealed class Circle(double radius) : Shape
{
    public override double Area() => Math.PI * radius * radius;
}

Shape shape = new Circle(5);
Console.WriteLine(shape.Area());
```

### 进阶示例
#### 示例 1：`new` 隐藏
```csharp
public class Base
{
    public virtual void Run() => Console.WriteLine("Base");
}

public class Derived : Base
{
    public new void Run() => Console.WriteLine("Derived hiding");
}

Base obj = new Derived();
obj.Run(); // 输出 Base
```
修正：使用 `override` 或重命名成员。

#### 示例 2：抽象模板方法
```csharp
public abstract class DataExporter
{
    public void Export() { Validate(); WriteData(); }
    protected abstract void WriteData();
    protected virtual void Validate() { }
}

public sealed class JsonExporter : DataExporter
{
    protected override void WriteData() => Console.WriteLine("Write JSON");
}
```

### 最佳实践
- 避免深继承层次，优先接口与组合。
- 在基类构造函数中仅初始化自身状态。
- 使用 `sealed override` 锁定继承链。

### 常见陷阱
1. **在构造函数中调用虚方法**：未初始化子类。
2. **滥用 `protected` 字段**：暴露实现细节。
3. **忽略 `base` 实现**：重写时忘记调用基类逻辑。

### 练习
1. 判断：抽象类可以有实例字段吗？
2. 简答：`sealed class` 的用途。
3. 编程：实现 `Shape` 子类 `Rectangle`。
4. 思考：里氏替换原则在 API 设计中的含义。
5. 改错：`public override void Run() { Run(); }`。

**参考答案**
1. 可以。
2. 阻止继承，提高安全或优化。
3. `public override double Area() => width * height;`。
4. 子类必须遵守基类契约，不改变可观察行为。
5. 递归调用导致栈溢出，应调用 `base.Run();`。

### 小结
- 继承是强力工具但需谨慎使用。
- 虚方法、抽象类、密封类形成可扩展骨架。
- 遵循里氏替换保障多态正确性。

### 参考链接/文档关键词
- "C# inheritance"
- "abstract vs virtual"
- "sealed override"
- "Liskov substitution"

## 第 10 章 接口 interface 与显式接口实现

### 本章目标
- 理解接口定义、实现与多重继承能力。
- 掌握显式接口实现的使用场景。
- 了解默认接口成员（C# 8）及兼容策略。
- 设计接口以实现解耦与可测试性。

### 关键术语
- 接口 *interface*：定义行为契约，无状态。
- 显式接口实现 *explicit interface implementation*：仅通过接口引用访问。
- 默认接口成员 *default interface member*：接口提供默认实现。
- 依赖倒置 *dependency inversion*：面向抽象编程。

### 核心概念与原理
- 接口可多继承，类型可以实现多个接口。接口成员默认 `public` 且无字段。
- 显式实现避免成员名冲突，常用于提供不同视角。
- 默认接口成员需在 .NET 5+ 与 C# 8+，旧运行时需回退为抽象类。

### 最小可运行示例
```bash
mkdir -p src/Chapter10.Interfaces
cd src/Chapter10.Interfaces
dotnet new console -n Chapter10.Interfaces -f net8.0
```

`Program.cs`：
```csharp
public interface ILogger
{
    void Log(string message);
}

public class ConsoleLogger : ILogger
{
    public void Log(string message) => Console.WriteLine(message);
}

ILogger logger = new ConsoleLogger();
logger.Log("Hello interface");
```

### 进阶示例
#### 示例 1：显式接口实现
```csharp
public interface ISerializer { string Serialize(object value); }
public interface ITextSerializer { string Serialize(string text); }

public class Serializer : ISerializer, ITextSerializer
{
    string ISerializer.Serialize(object value) => JsonSerializer.Serialize(value);
    string ITextSerializer.Serialize(string text) => text.ToUpperInvariant();
}

ISerializer serializer = new Serializer();
Console.WriteLine(serializer.Serialize(new { Name = "Alice" }));
```

#### 示例 2：默认接口成员
```csharp
public interface IClock
{
    DateTime Now => DateTime.UtcNow;
    virtual string FormatNow() => Now.ToString("O");
}

public class CustomClock : IClock
{
    public DateTime Now => DateTimeOffset.Now.DateTime;
    public string FormatNow() => Now.ToString("HH:mm:ss");
}
```

### 最佳实践
- 接口命名以 `I` 前缀（如 `ILogger`）。
- 根据领域划分接口，避免胖接口。
- 在依赖注入容器中注册接口与实现。
- 向旧平台发布时避免默认成员，使用抽象基类替代。

### 常见陷阱
1. **接口变化破坏兼容**：添加成员将破坏二进制兼容。
2. **显式实现难以测试**：需要转换接口类型，使用适配器简化。
3. **默认成员滥用**：复杂逻辑应放在实现而非接口。

### 练习
1. 判断：接口可以包含字段吗？
2. 简答：显式接口实现的适用场景。
3. 编程：创建 `IRepository<T>` 与 `InMemoryRepository<T>`。
4. 思考：接口与抽象类如何选择？
5. 改错：为何 `new Serializer().Serialize("text")` 编译失败？

**参考答案**
1. 否。
2. 解决命名冲突或隐藏实现细节。
3. 使用 `Dictionary` 存储并实现增删查。
4. 接口定义能力，抽象类共享实现。
5. `Serialize` 为显式实现，需要转换到 `ITextSerializer`。

### 小结
- 接口提供多态解耦能力。
- 显式实现用于解决冲突与封装细节。
- 默认接口成员带来演进灵活性，但需兼容考虑。

### 参考链接/文档关键词
- "C# interface"
- "explicit interface implementation"
- "default interface members"
- "Dependency inversion"

