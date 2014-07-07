title: piqi项目2
date: 2014-02-02 18:18:30
updated : 
permalink: 
tags:
categories:
-  FAQ
---
[示例](#examples) // [局限性](#limitations) // [入门](#howtogetstarted) // [项目进展](#projectstatus)

![](/images/piqi-small.png)

Piqi (/pɪki/)是一种schema语言,与之对应有一些工具.

Piqi语言可以用在为JSON,XML,Google Protocol Buffer等数据格式定义schema.

Piqi的子项目包括:

*   用以校验 格式化和在JSON,XML,Protocol Buffer格式间互相转换的命令行工具.

*   针对[Erlang](https://github.com/alavrik/piqi-erlang) and [OCaml](https://github.com/alavrik/piqi-ocaml)的多种格式的数据序列化程序.

*   Piq-对人友好的类型化数据表达语言. 它设计的初衷在于,与JSON XML CSV,S表达式和其他格式相比,浏览/编辑数据更加方便.

*   Piqi-RPC-针对Erlang的RPC-HTTP库.它提供了一种简单的方式来构建基于HTTP的JSON XML Protocol Buffer的Erlang服务.     

Piqi项目受Google Protocol Buffers的启发,设计之初就在很大程度上兼容Google Protocol Buffers. 和Google Protocol Buffers类似,Piqi依赖类型定义,支持schema演化.主要的差异在于Piqi拥有一个更为强大的数据模型,高等级的模块,与JSON XML之间的标准映射,也有强大的数据表达格式Piq.同时,Piqi扩展性更强.

更多Piqi与其他程序的对比信息可以参考[Rationale](/rationale/) and [FAQ](/faq/) . Protocol Buffers 和 Piqi 的兼容性[请参考](/doc/protobuf/).

##  组件和子项目

如下是对Piqi组件和子项目的概述.


**Piqi- 一种schema语言** (文件后缀名为`.piqi` )


Piqi可以用作JSON, XML, Protocol Bufferss 和 Piq的schema语言.

Piqi支持对record\varaiant[tagged unions](http://en.wikipedia.org/wiki/Tagged_union))\enum\list和type aliase的定义.

Piqi支持高级模块和从其他模块中导入/包含定义的机制.

Piqi的类型定义是可扩展的,在保持前后兼容的情况下,支持schema的演化.

数据模型,扩展性和模块引入的结合使得Piqi成为自定义语言.地自定义的特性本身就很好,同时也有利于Piqi的实现,使得语言的扩展性增强.

Piqi(`.piqi` 文件中定义) 的模块和类型可以转换为Google Protocol Buffers类型标准(`.proto` files),反之亦然.

Piqi的模块可以用Protocol Buffers, JSON and XML格式来表达. 这样其他程序能够就简单的与Piqi类型定义整合在一起.

[(Piqi的完整特性列表)](/doc/piqi/#overview)

**Piq -一种数据表达语言** (文件后缀为`.piq`)


Piq是一种基于文本的语言,能够让人很容易地读写和编辑结构化数据. 

它的语法很简明 很强大 能够表达诸如数字 布尔值 字符串 二进制流 列表和自由文本等多种数据对象.

Piq是一种流格式,也就是说一份`.piq`文件可以包含多个Piq 对象. 除了数据之外, Piq 流还能够以内嵌Piqi模块的方式引入/包含类型定义.

[(Piqi的完整特性列表)](/doc/piqi/#overview)


**编程语言对应的序列化程序**


Piqi通过[Google Protocol Buffers](/doc/protobuf/)和使用[OCaml](/doc/ocaml/) and [Erlang](/doc/erlang/)实现提供了对编程语言的静态映射.

Protocol Buffers官方支持Python, Java and C++.也有一些诸如C#, Go, Common Lisp, Scala, Clojure等编程语言的[第三方库](http://code.google.com/p/protobuf/wiki/ThirdPartyAddOns).

诸如JavaScript等动态编程语言也能够使用JSON or XML [编码](/doc/encodings/) 的数据.


**Piq and Piqi的命令行工具**


`piqi` 静态可执行程序,实现了以下命令:

`piqi convert`    Piq, JSON, XML and Protocol Buffers 格式的结构化数据之间的转换.

`piqi check`   校验 `.piq` and `.piqi` 的有效性

`piqi pp`   格式化 `.piq` and `.piqi` 文件

`piqi to-proto`, `piqi of-proto`   `.piqi` 与 `.proto`之间的转换

[(更多Piqi工具)](/doc/tools/)


**Piqi-RPC: 基于HTTP 的RPC程序 for Erlang**


Piqi-RPC为Erlang开发让你有提供了一种简便可靠的方式,通过使用基于HTTP的JSON, XML or Google Protocol Buffers,将基于Erlang编写的服务与其他非Erlang的客户端集成起来.

同时也包含了`piqi call`  通过命令行远程调用Piqi-RPC Erlang函数的客户端. `piqi call` 获取命令行参数,将参数转换为远程函数的入参.

[(Piqi-RPC相关的更多信息)](/doc/piqi-rpc/)



##<a name="examples"/>Examples

如下是两个示例:

*   `person.piq` 是表示一个addressbook的Piq文件 其中包含了两个person的record记录.

*   `person.piqi` 是一个Piqi模块,包含了对person record类型的定义.

详细信息参见 [示例](/examples/) page.

[person.piqi](#person_piqi)

*   [Source](#person_piqi_source)

```
% definition of a record type
.record [
    .name person      % record name
    .field [
        .name name    % field name
        .type string  % field type
    ]
    .field [
        .name id
        .type int
    ]
    .field [
        .name email
        .type string
        .optional     % field is optional
    ]
    .field [
        .name phone
        .type phone-number
        .repeated     % field can be repeated 0 or more times
    ]
]

.record [
    .name phone-number
    .field [
        .name number
        .type string
    ]
    .field [
        .name type
        .type phone-type
        .optional
        .default.home  % default value for an optional field

        % ".default.home" is a shorthand for ".default (.home)", where
        % ".home" is a value of the enum type defined below
    ]
]

% definition of an enum type
.enum [
    .name phone-type
    .option [ .name mobile ]
    .option [ .name home ]
    .option [ .name work ]
]
```
*   [Piqi.Proto](#person_piqi_proto)

```
message person {
    required string name = 1;
    required sint32 id = 2;
    optional string email = 3;
    repeated phone_number phone = 4;
}

message phone_number {
    required string number = 1;
    optional phone_type type = 2 [default = home];
}

enum phone_type {
    mobile = 1;
    home = 2;
    work = 3;
}

```
*   [Piqi.JSON](#person_piqi_json)

```
{
  "piqi_type": "piqi",
  "module": "person",
  "typedef": [
    {
      "record": {
        "name": "person",
        "field": [
          { "name": "name", "type": "string", "mode": "required" },
          { "name": "id", "type": "int", "mode": "required" },
          { "name": "email", "type": "string", "mode": "optional" },
          { "name": "phone", "type": "phone-number", "mode": "repeated" }
        ]
      }
    },
    {
      "record": {
        "name": "phone-number",
        "field": [
          { "name": "number", "type": "string", "mode": "required" },
          {
            "name": "type",
            "type": "phone-type",
            "mode": "optional",
            "default": "home"
          }
        ]
      }
    },
    {
      "enum": {
        "name": "phone-type",
        "option": [
          { "name": "mobile" },
          { "name": "home" },
          { "name": "work" }
        ]
      }
    }
  ]
}
```
*   [Piqi.XML](#person_piqi_xml)

```
<?xml version="1.0" encoding="UTF-8"?>
<value>
  <module>person</module>
  <typedef>
    <record>
      <name>person</name>
      <field>
        <name>name</name>
        <type>string</type>
        <mode>required</mode>
      </field>
      <field>
        <name>id</name>
        <type>int</type>
        <mode>required</mode>
      </field>
      <field>
        <name>email</name>
        <type>string</type>
        <mode>optional</mode>
      </field>
      <field>
        <name>phone</name>
        <type>phone-number</type>
        <mode>repeated</mode>
      </field>
    </record>
  </typedef>
  <typedef>
    <record>
      <name>phone-number</name>
      <field>
        <name>number</name>
        <type>string</type>
        <mode>required</mode>
      </field>
      <field>
        <name>type</name>
        <type>phone-type</type>
        <mode>optional</mode>
        <default>home</default>
      </field>
    </record>
  </typedef>
  <typedef>
    <enum>
      <name>phone-type</name>
      <option>
        <name>mobile</name>
      </option>
      <option>
        <name>home</name>
      </option>
      <option>
        <name>work</name>
      </option>
    </enum>
  </typedef>
</value>
```
*   [Piqi-light](#person_piqi_light)

```
type person =
  {
    - name :: string()
    - id :: int()
    ? email :: string()
    * phone :: phone-number()
  }

type phone-number =
  {
    - number :: string()
    ? type :: phone-type() = .home
  }

type phone-type =
    | mobile
    | home
    | work
```
[person.piq](#person_piq)

*   [Source](#person_piq_source)

```
    % this is an object of type "person" which is defined in module "person"
    :person/person [
        .name "J. Random Hacker"
        .id 0

        .email "j.r.hacker@example.com"

        .phone [
            .number "(111) 123 45 67"
            % NOTE: phone is "home" by default
        ]

        .phone [
            .number "(222) 123 45 67"
            .mobile
        ]

        .phone [
            .number "(333) 123 45 67"
            .work
        ]
    ]

    % another object of the same type
    :person/person [
        .name "Joe User"
        .id 1

        % Joe User doesn't have an email

        .phone [ "(444) 123 45 67" ]
        .phone [ "(555) 123 45 67" .work ]
    ]
```
*   [Piq](#person_piq_piq)

```
    :person/person [
        .name "J. Random Hacker"
        .id 0
        .email "j.r.hacker@example.com"
        .phone [ .number "(111) 123 45 67" ]
        .phone [
            .number "(222) 123 45 67"
            .type.mobile
        ]
        .phone [
            .number "(333) 123 45 67"
            .type.work
        ]
    ]

    :person/person [
        .name "Joe User"
        .id 1
        .phone [ .number "(444) 123 45 67" ]
        .phone [
            .number "(555) 123 45 67"
            .type.work
        ]
    ]
```
*   [JSON](#person_piq_json)

```
    {
      "piqi_type": "person/person",
      "name": "J. Random Hacker",
      "id": 0,
      "email": "j.r.hacker@example.com",
      "phone": [
        { "number": "(111) 123 45 67", "type": "home" },
        { "number": "(222) 123 45 67", "type": "mobile" },
        { "number": "(333) 123 45 67", "type": "work" }
      ]
    }

    {
      "piqi_type": "person/person",
      "name": "Joe User",
      "id": 1,
      "phone": [
        { "number": "(444) 123 45 67", "type": "home" },
        { "number": "(555) 123 45 67", "type": "work" }
      ]
    }
```
*   [XML](#person_piq_xml)

```
<?xml version="1.0" encoding="UTF-8"?>
<value>
  <name>J. Random Hacker</name>
  <id>0</id>
  <email>j.r.hacker@example.com</email>
  <phone>
    <number>(111) 123 45 67</number>
    <type>home</type>
  </phone>
  <phone>
    <number>(222) 123 45 67</number>
    <type>mobile</type>
  </phone>
  <phone>
    <number>(333) 123 45 67</number>
    <type>work</type>
  </phone>
</value>

<?xml version="1.0" encoding="UTF-8"?>
<value>
  <name>Joe User</name>
  <id>1</id>
  <phone>
    <number>(444) 123 45 67</number>
    <type>home</type>
  </phone>
  <phone>
    <number>(555) 123 45 67</number>
    <type>work</type>
  </phone>
</value>
```
*   [Piq (with embedded Piqi)](#person_piq_piq_embedded)
   
```                                       
    :piqi [
        .module person
        .record [
            .name person
            .field [
                .name name
                .type string
            ]
            .field [
                .name id
                .type int
            ]
            .field [
                .name email
                .type string
                .optional
            ]
            .field [
                .name phone
                .type phone-number
                .repeated
            ]
        ]
        .record [
            .name phone-number
            .field [
                .name number
                .type string
            ]
            .field [
                .name type
                .type phone-type
                .optional
                .default.home
            ]
        ]
        .enum [
            .name phone-type
            .option [ .name mobile ]
            .option [ .name home ]
            .option [ .name work ]
        ]
    ]
    :person/person [
        .name "J. Random Hacker"
        .id 0
        .email "j.r.hacker@example.com"
        .phone [ .number "(111) 123 45 67" ]
        .phone [
            .number "(222) 123 45 67"
            .type.mobile
        ]
        .phone [
            .number "(333) 123 45 67"
            .type.work
        ]
    ]

    :person/person [
        .name "Joe User"
        .id 1
        .phone [ .number "(444) 123 45 67" ]
        .phone [
            .number "(555) 123 45 67"
            .type.work
        ]
    ]
```
*   [Pib](#person_piq_pib)  

```
    0000000: faff ffff 0f1c 0a09 7069 7169 2d74 7970  ........piqi-typ
    0000010: 6512 0d70 6572 736f 6e2f 7065 7273 6f6e  e..person/person
    0000020: 1802 1269 0a10 4a2e 2052 616e 646f 6d20  ...i..J. Random 
    0000030: 4861 636b 6572 1000 1a16 6a2e 722e 6861  Hacker....j.r.ha
    0000040: 636b 6572 4065 7861 6d70 6c65 2e63 6f6d  cker@example.com
    0000050: 2211 0a0f 2831 3131 2920 3132 3320 3435  "...(111) 123 45
    0000060: 2036 3722 130a 0f28 3232 3229 2031 3233   67"...(222) 123
    0000070: 2034 3520 3637 1001 2213 0a0f 2833 3333   45 67.."...(333
    0000080: 2920 3132 3320 3435 2036 3710 0312 340a  ) 123 45 67...4.
    0000090: 084a 6f65 2055 7365 7210 0222 110a 0f28  .Joe User.."...(
    00000a0: 3434 3429 2031 3233 2034 3520 3637 2213  444) 123 45 67".
    00000b0: 0a0f 2835 3535 2920 3132 3320 3435 2036  ..(555) 123 45 6
    00000c0: 3710 03                                  7..
```

##<a name="limitations"/>局限性

*  与XML不同的是, Piqi 不支持半结构化数据,没有查询和转换语言(有一些这方面的 [计划](/roadmap/)). 同时,能够使用XPath, XSLT and XQuery来处理XML格式的数据 或者是 [jq](http://stedolan.github.com/jq/)等工具来处理JSON数据.

*   目前,Piqi语言的实现和Piqi的根据都被打包成一个单独的命令行工具,除了Erlang和OCaml以外,并不能作为第三方库来使用.

## <a name="howtogetstarted"/>如何入门

阅读[文档](/doc/)了解更多Piqi信息, 学习[范例](/examples/).

[下载](/downloads/)工具或者从源代码开始编译 Piqi工具.

跟踪 [GitHub项目](http://github.com/alavrik/piqi)或者[订阅最新消息](http://piqi.org/blog/).

如果你有任何问题或建议,欢迎到[Piqi Google Group](http://groups.google.com/group/piqi)或者 邮箱[alavrik@piqi.org](mailto:alavrik@piqi.org) twitter[@alavrik](http://twitter.com/alavrik).

如果你发现一个bug,请提交至[GitHub issue](http://github.com/alavrik/piqi/issues).

欢迎大家的反馈和参与! If you find Piqi useful in some way or another, please drop me a line.

## <a name="projectstatus"/>项目进展

Piqi 还处于Beta版.

已经在Linux和Mac OS X平台上经过测试. 其他Unix系统也应该能够运行.比如, Piqi能够运行在 FreeBSD 和 Solaris/x86. Windows上可以利用MinGW and Cygwin来编译Piqi.详细信息参考[安装指南](http://github.com/alavrik/piqi/blob/master/INSTALL) .

查阅[Roadmap page](/roadmap/),查看Piqi计划实现的特性. 

版权所有 2010-2014 [Anton Lavrik](mailto:alavrik@piqi.org)

    Except where otherwise noted the content of this website is licensed under a  [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/).