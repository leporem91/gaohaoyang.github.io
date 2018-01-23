---
layout: post
title:  "C# Language"
date:   2015-01-02 17:04:00
categories: C# Language
tags: C#
---

* content
{:toc}

C# 프로그래밍 기초 문법
도서(뇌를 자극하는 C# 4.0 프로그래밍 - 박상현 저)의 내용을 정리합니다. 

## .NET Framework (닷넷 프레임워크)

C# 이라고 하면  항상 .NET Framework 에 대한 얘기가 나오곤 합니다.

.NET Framework 는 Microsoft에서 개발한 웹 기반, 윈도우 기반 application을 개발할 수 있고, 실행시킬 수 있는 프레임워크이며, .NET 표준에 따르는 프로그래밍 언어로 개발된 프로그램의 실행환경이라고 할 수 있습니다.

.NET Framework의 구성을 그림으로 보면 다음과 같습니다.

![](/_images/01.NET_framework/1-1.png)

위에서 하나씩 살펴보자면

여기서 .NET 표준을 따르는 (CLS; Common Language Specification)을 따르는 여러 언어를 제공합니다.

(대표적으로 C# 외에 VB.NET , Managed C++ , Jscript.NET , j # 등이 있다.)


Class Library 구성을 보면 다음과 같습니다.
ASP.NET Web Forms Web Services : Web service와 Web apps를 개발
Windows Forms : Windows 프로그래밍
ADO .NET and XML : XML 및 데이터베이스 활용
Base Class Library : CLR 지원을 위한 핵심 클래스 라이브러리

### Common Language Runtime (CLR)

.NET 언어로 작성된 프로그램을 실행하고 관리하는 실행환경이며 Java의 virtual machine에 해당한다고 볼 수 있습니다.
CLR은 .NET에서 동작하는 프로그램을 적재하고, 프로그램의 동적 컴파일, 프로그램의 실행, 메모리관리 (Garbage Collection) ,프로그램의 예외처리, 언어 간의 상속 지원, COM과의 상호 운영성 지원 등을 가능케 합니다.
.NET 언어라 하면 C#뿐만 아니라 위에서 나열하였던 VB.NET 등 .NET 표준을 따르는 여러언어들은 CLR을 통해 프로그램을 실행할 수 있게 됩니다.

![](/_images/01.NET_framework/1-2png)

 이것이 가능한 이유는 Intermediate Language (IL, 중간언어) 라는 기계어로 변환하기 쉬운 상태의 중간 단계의 언어로 .NET에서 번역되어 실행되기 위해 IL형태로 컴파일을 하는데, IL을 기계어로 바꾸는 번역기만 제공되면 어떤 플랫폼에서도 실행가능합니다. JIT (Just-In-Time) 컴파일러를 통해 IL을 동적으로 컴파일하는데 .NET 에서는 이와같이 프로그램을 2번 컴파일 합니다. Assembly는 이 때 IL로 컴파일된 결과 파일들을 패키징 한 것을 말합니다.
(.exe는 여러개의 class와 Main프로그램을 포함하고, dll은 class만을 포함한다고 생각하면 된다.)
또 .NET 언어가 지켜야 하는 스펙으로 Common Language Specifications (CLS) 로 다른 .NET 언어로 작성된 것도 호환되어 동작 가능하게 합니다. 이 과정에서 Common Type System (CTS) 라는 .NET 언어마다 Data type이 다를 수 있는데,이를 언어나 시스템 환경에 관계없이 동일한 Data type을 유지하기 위한 규약이 사용되기도 합니다.

쉽게 요약하면, C# 컴파일러는 우리가 작성한 코드를 IL로 작성된 실행파일을 만들게 되고, 이 파일을 실행시키면 CLR이 IL을 읽어 다시 OS에 이해할수 있는 코드로 컴파일하여 실행시킵니다. 이렇게 서로 다른 언어가 만나는 지점이 IL언어이고, CLR이 다시 자신이 설치되어 있는 플랫폼에 최적화시켜 컴파일한 후 실행하게 됩니다.
이렇게 플랫폼에 최적화된 코드를 만들어 내는 장점이 있으나, 단점은 실행시에 이루어지는 컴파일의 비용부담이 되겠습니다.

## 데이터 다루기

**데이터 형식 (Data Type)**

C#에서 제공하는 데이터 형식은 숫자, 텍스트 뿐만 아니라, 이미지, 소리까지 다룰 수 있는 데이터 형식을 제공합니다.
데이터 형식은 기본 데이터형식(Primitive Type) 과 복합 데이터형식 (Complex Data Type) 으로 나눌 수 있습니다.
기본 데이터형식은 흔히 생각하는 int , double 과 같은 개념이라 생각하면 되고,
복합 데이터형식은 기본데이터 형식을 기본으로 하는 구조체나 클래스 등이 되겠습니다.
기본 데이터형식과 복합 데이터형식을 다시 값 형식과 참조 형식으로 분류할 수 있습니다.


**값 형식 (Value Types), 참조 형식 (Reference Types)**

값 형식은 메모리 영역 중 스택(Stack) 영역 에 저장되며, 선언 되었던 코드 블록이 끝나면 스택영역에서 데이터가 제거됩니다.
스택에 쌓인 데이터들이 코드 블록이 끝나는 순간 제거 된다는 것은 값 형식의 장점이자 단점이 됩니다.

코드 블록이 끝나는 순간 데이터가 제거되기 때문에 메모리영역이 전부 회수되지만, 코드 블록안에서만 사용가능합니다.

참조 형식은 메모리 영역 중 힙(Heap) 영역에 데이터를 저장하는데, 힙 영역은 코드 블록과 상관 없이 데이터는 사라지지 않습니다. 참조 형식의 변수는 힙과 스택을 동시에 이용합니다. 힙 영역에는 데이터의 값을 저장하고, 스택 영역에는 이 데이터의 주소를 저장합니다. 스택 영역은 코드 블록이 끝나는 순간 사라지지만 ( 데이터의 주소), 힙 영역에 데이터의 값은 사라지지 않습니다. C# 에서는 CLR의 가비지 컬렉터 (Garbage Collector) 가 힙에 사용하지 않는 객체를 자동으로 제거해줍니다.

**object 형식**

 C#은 모든 데이터 형식을 다룰 수 있는 object형식이 존재합니다. 모든 데이터 형식 ( 기본 데이터 형식 뿐만 아니라 모든 복합 데이터 형식, 프로그래머가 만드는 데이터형식 까지도) 자동으로 object 형식으로부터 상속받게 하였기 때문입니다.

정수 형식은 short 와 int 의 처리가 다르고, 부동 소수점 형식은 float 와 double 가 처리가 다른데도 가능한 이유는 박싱(boxing) 과 언박싱(unboxing) 이라는 메커니즘이 있기 때문입니다.

**박싱(boxing), 언박싱(unboxing)**

object 형식은 참조 형식이기 때문에 힙에 데이터를 할당합니다.
하지만 object 형식에 값 형식의 데이터 (int와 같은)를 할당하면 object 형식은 박싱을 수행해서 데이터를 힙에 할당합니다. 이 object 형식을 다시 값 형식의 변수에 할당하면, object 형식의 데이터를 언박싱하여 데이터 값을 값 형식의 변수에 할당합니다.

예를 들어, 다음과 같은 코드가 있습니다.
```
object a= 10;
int b = (int) a;
```
이럴 경우 10을 박싱하여 힙에 저장하고, a는 박싱한 10의 주소를 갖습니다. 다시 b에 저장하고자 할때 a는 언박싱 되어 10이 b에 저장됩니다.

**열거 형식(Enumerator)**

종류는 같지만, 다른 값을 갖는 상수들을 선언해야 할때 유용합니다.

예를 들면, 메시지 박스를 띄웠을 때 사용자로 부터 받는 응답이 Yes, No, Cancel 과 같을 때 상수로 선언하여 컨트롤하면 쉽습니다.
```
enum 열거형식명 : 기반자료형 { 상수1, 상수2, .... }
```
기반 자료형은 정수 계열(byte, short, int, long 등)만 사용할 수 있습니다. 생략할 경우 컴파일러가 int 형으로 사용합니다. 

enum 의 여러가지 사용방법은 다음과 같습니다.

``` Csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
 
namespace CsharpStudy
{
    class Program
    {
        enum DialogResult { YES=1 , NO , CANCEL }
 
        static void Main(string[] args)
        {
            Console.WriteLine(DialogResult.YES);
            Console.WriteLine(DialogResult.NO);
            Console.WriteLine(DialogResult.CANCEL);
            Console.WriteLine();
            Console.WriteLine((int)DialogResult.YES);
            Console.WriteLine((int)DialogResult.NO);
            Console.WriteLine((int)DialogResult.CANCEL);
            Console.WriteLine();
            Console.WriteLine( (DialogResult) 1);
            Console.WriteLine( (DialogResult) 2);
            Console.WriteLine( (DialogResult) 3);
        }
    }
}
```



---

最后补充一点设计模式相关的资料，我还没有来得及看的：

* [学用 JavaScript 设计模式](http://www.oschina.net/translate/learning-javascript-design-patterns)
* [常用的Javascript设计模式](http://blog.jobbole.com/29454/)
* [JavaScript设计模式深入分析](http://developer.51cto.com/art/201109/288650_all.htm)
