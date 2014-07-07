title: piqi 项目
date: 2014-06-13 16:08:30
updated : 
permalink: 
tags:
categories:
-  实例
-------------
# [piqi 项目](http://piqi.org/)
**目录**

[TOC]


##     Piq and Piqi 示例    ##

这部分包含了`.piq`和`piqi`文件的示例.  

数据(.piq文件)和数据定义(.piqi文件)有多种展现格式:  

*   **Source**—源代码.  
*   **Piq**-经由`piqi convert`命令对source文件处理得到的Piq文件.  
*   **JSON**-经由`piqi convert -t json`命令对原始Piq文件处理得到的JSON格式.  
*   **XML**-经由`piqi convert -t xml`命令对原始Piq文件处理得到的XML格式.  
*   **Piq (with embedded Piqi)**-与**Piq**类似,但是其中内嵌了定义Piq流中数据类型的Piqi模块,通过`piqi convert --embed-piqi -t piq`.  
*   **Pib**-Binary representation of the Piq file produced by `piqi convert -t pib`.
*   **Piqi.Proto**-通过`piqi to-proto`命令得到的Protocol Buffers 数据定义.  
*   **Proto.Piqi**-通过`piqi of-proto`命令对Protocol Buffers `.proto`文件处理得到的Piqi类型定义/规范.  
*   **Piqi-light**-轻量级的Piqi语法表示的Piqi类型定义/规范.  

[Piqi标准](/self-definition/)包含了用来定义Piqi语言自身的实例.   
(Examples listed below can be also found in Piqi [sources](http://github.com/alavrik/piqi/tree/master/examples/).)
<div id="accordion">
###    Piq基本类型和基本语法元素    ###


####    comment.piq    ####
*   [Source](#comment_piq_source)
*   [Piq](#comment_piq_piq)
*   [JSON](#comment_piq_json)
*   [XML](#comment_piq_xml)
*   [Piq (with embedded Piqi)](#comment_piq_piq_embedded)
*   [Pib](#comment_piq_pib)

<a name="comment_piq_source"/>
```
% This is an empty .piq file with a bunch of comments

% comments start with '%' character and continue until the end of the line

% one
% two
% three

% Note that '%%' is not a valid literal sequence.
%
```
<a name="comment_piq_piq"/>
<a name="comment_piq_json"/>
<a name="comment_piq_xml"/>
<a name="comment_piq_piq_embedded"/>
<a name="comment_piq_pib"/>
####    bool.piq    ####

*   [Source](#bool_piq_source)
*   [Piq](#bool_piq_piq)
*   [JSON](#bool_piq_json)
*   [XML](#bool_piq_xml)
*   [Piq (with embedded Piqi)](#bool_piq_piq_embedded)
*   [Pib](#bool_piq_pib)
<a name="bool_piq_source"/>
```
        (:bool)

        true false

        :def/r [
            .i 0

            .bool true
        ]

        :def/r [
            .i 0

            .bool false
        ]

        :def/r [
            .i 0

            % same as .bool true
            .bool
        ]
```
<a name="bool_piq_piq"/>

```
        (:bool)

        true

        false

        :def/r [
            .i 0
            .bool true
        ]

        :def/r [
            .i 0
            .bool false
        ]

        :def/r [
            .i 0
            .bool true
        ]
```
<a name="bool_piq_json"/>

```
        { "piqi_type": "bool", "value": true }

        { "piqi_type": "bool", "value": false }

        { "piqi_type": "def/r", "i": 0, "b": "YWJjIP8A", "bool": true }

        { "piqi_type": "def/r", "i": 0, "b": "YWJjIP8A", "bool": false }

        { "piqi_type": "def/r", "i": 0, "b": "YWJjIP8A", "bool": true }
```
<a name="bool_piq_xml"/>

```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>true</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>false</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <i>0</i>
          <b>YWJjIP8A</b>
          <bool>true</bool>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <i>0</i>
          <b>YWJjIP8A</b>
          <bool>false</bool>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <i>0</i>
          <b>YWJjIP8A</b>
          <bool>true</bool>
        </value>

```
<a name="bool_piq_piq_embedded"/>
```
        (:bool)

        true

        false

        :piqi [
            .module def
            .record [
                .name r
                .field [
                    .name i
                    .type int
                ]
                .field [
                    .name s
                    .type string
                    .optional
                ]
                .field [
                    .name b
                    .type binary
                    .optional
                    .default "abc \xff\x00"
                ]
                .field [
                    .name f
                    .type float
                    .repeated
                ]
                .field [
                    .name flag
                    .optional
                ]
                .field [
                    .type bool
                    .optional
                ]
                .field [
                    .name self
                    .type r
                    .optional
                ]
                .field [
                    .type v
                    .optional
                ]
            ]
            .enum [
                .name e
                .option [
                    .name a
                    .protobuf-name "e_a"
                ]
                .option [ .name b ]
                .option [ .name c ]
            ]
            .variant [
                .name v
                .option [
                    .name i
                    .type int
                ]
                .option [ .type r ]
                .option [ .type e ]
                .option [ .name flag ]
                .option [
                    .name l
                    .type v-list
                ]
            ]
            .alias [
                .name a
                .type v
            ]
            .alias [
                .name uuid
                .type binary
            ]
            .alias [
                .name epoch-seconds
                .type uint64
            ]
            .list [
                .name v-list
                .type v
            ]
            .list [
                .name int-list
                .type int
            ]
            .list [
                .name int-list-list
                .type int-list
            ]
        ]

        :def/r [
            .i 0
            .bool true
        ]

        :def/r [
            .i 0
            .bool false
        ]

        :def/r [
            .i 0
            .bool true
        ]

```
<a name="bool_piq_pib"/>

```



        0000000: faff ffff 0f13 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0462 6f6f 6c18 0108 0108 00fa ffff  e..bool.........
        0000020: ff0f 140a 0970 6971 692d 7479 7065 1205  .....piqi-type..
        0000030: 6465 662f 7218 0212 0408 0030 0112 0408  def/r......0....
        0000040: 0030 0012 0408 0030 01                   .0.....0.
```
####    int.piq    ####

*   [Source](#int_piq_source)
*   [Piq](#int_piq_piq)
*   [JSON](#int_piq_json)
*   [XML](#int_piq_xml)
*   [Piq (with embedded Piqi)](#int_piq_piq_embedded)
*   [Pib](#int_piq_pib)

<a name="int_piq_source"/>
```
        % examples of integer values
        (:int)

        0 -1 100 1_000_000_000 

        % NOTE: unsigned integers use different binary encoding
        :uint 100

        % conventional base 16 integers

        0xffff -0xffff_0000

        % base 2 integer literal

        0b1111_1111_1111_1111

        % min and max values for various integer types/encodings

        :uint32 0
        :uint32 0xffff_ffff

        :uint32-fixed 0
        :uint32-fixed 0xffff_ffff

        :int32 -0x8000_0000
        :int32 0x7fff_ffff

        :int32-fixed -0x8000_0000
        :int32-fixed 0x7fff_ffff

        :protobuf-int32 -0x8000_0000
        :protobuf-int32 0x7fff_ffff

        :uint64 0
        :uint64 0xffff_ffff_ffff_ffff

        :uint64-fixed 0
        :uint64-fixed 0xffff_ffff_ffff_ffff

        :int64 -0x8000_0000_0000_0000
        :int64 0x7fff_ffff_ffff_ffff

        :int64-fixed -0x8000_0000_0000_0000
        :int64-fixed 0x7fff_ffff_ffff_ffff

        :protobuf-int64 -0x8000_0000_0000_0000
        :protobuf-int64 0x7fff_ffff_ffff_ffff

```
<a name="int_piq_piq"/>
```

        (:int)

        0

        -1

        100

        1000000000

        :uint 100

        65535

        -4294901760

        65535

        :uint32 0

        :uint32 4294967295

        :uint32-fixed 0

        :uint32-fixed 4294967295

        :int32 -2147483648

        :int32 2147483647

        :int32-fixed -2147483648

        :int32-fixed 2147483647

        :protobuf-int32 -2147483648

        :protobuf-int32 2147483647

        :uint64 0

        :uint64 0xffffffffffffffff

        :uint64-fixed 0

        :uint64-fixed 0xffffffffffffffff

        :int64 -9223372036854775808

        :int64 9223372036854775807

        :int64-fixed -9223372036854775808

        :int64-fixed 9223372036854775807

        :protobuf-int64 -9223372036854775808

        :protobuf-int64 9223372036854775807
```
<a name="int_piq_json"/>
```
        { "piqi_type": "int", "value": 0 }

        { "piqi_type": "int", "value": -1 }

        { "piqi_type": "int", "value": 100 }

        { "piqi_type": "int", "value": 1000000000 }

        { "piqi_type": "uint", "value": 100 }

        { "piqi_type": "int", "value": 65535 }

        { "piqi_type": "int", "value": -4294901760 }

        { "piqi_type": "int", "value": 65535 }

        { "piqi_type": "uint32", "value": 0 }

        { "piqi_type": "uint32", "value": 4294967295 }

        { "piqi_type": "uint32-fixed", "value": 0 }

        { "piqi_type": "uint32-fixed", "value": 4294967295 }

        { "piqi_type": "int32", "value": -2147483648 }

        { "piqi_type": "int32", "value": 2147483647 }

        { "piqi_type": "int32-fixed", "value": -2147483648 }

        { "piqi_type": "int32-fixed", "value": 2147483647 }

        { "piqi_type": "protobuf-int32", "value": -2147483648 }

        { "piqi_type": "protobuf-int32", "value": 2147483647 }

        { "piqi_type": "uint64", "value": 0 }

        { "piqi_type": "uint64", "value": 18446744073709551615 }

        { "piqi_type": "uint64-fixed", "value": 0 }

        { "piqi_type": "uint64-fixed", "value": 18446744073709551615 }

        { "piqi_type": "int64", "value": -9223372036854775808 }

        { "piqi_type": "int64", "value": 9223372036854775807 }

        { "piqi_type": "int64-fixed", "value": -9223372036854775808 }

        { "piqi_type": "int64-fixed", "value": 9223372036854775807 }

        { "piqi_type": "protobuf-int64", "value": -9223372036854775808 }

        { "piqi_type": "protobuf-int64", "value": 9223372036854775807 }

```
<a name="int_piq_xml"/>

```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-1</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>100</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>1000000000</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>100</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>65535</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-4294901760</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>65535</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>4294967295</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>4294967295</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-2147483648</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>2147483647</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-2147483648</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>2147483647</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-2147483648</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>2147483647</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>18446744073709551615</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>18446744073709551615</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-9223372036854775808</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>9223372036854775807</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-9223372036854775808</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>9223372036854775807</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-9223372036854775808</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>9223372036854775807</value>
```
<a name="int_piq_piq_embedded"/>

```
        (:int)

        0

        -1

        100

        1000000000

        :uint 100

        65535

        -4294901760

        65535

        :uint32 0

        :uint32 4294967295

        :uint32-fixed 0

        :uint32-fixed 4294967295

        :int32 -2147483648

        :int32 2147483647

        :int32-fixed -2147483648

        :int32-fixed 2147483647

        :protobuf-int32 -2147483648

        :protobuf-int32 2147483647

        :uint64 0

        :uint64 0xffffffffffffffff

        :uint64-fixed 0

        :uint64-fixed 0xffffffffffffffff

        :int64 -9223372036854775808

        :int64 9223372036854775807

        :int64-fixed -9223372036854775808

        :int64-fixed 9223372036854775807

        :protobuf-int64 -9223372036854775808

        :protobuf-int64 9223372036854775807
```

<a name="int_piq_pib"/>


```
        0000000: faff ffff 0f12 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0369 6e74 1801 0800 0801 08c8 0108  e..int..........
        0000020: 80a8 d6b9 07fa ffff ff0f 130a 0970 6971  .............piq
        0000030: 692d 7479 7065 1204 7569 6e74 1802 1064  i-type..uint...d
        0000040: 08fe ff07 08ff fff7 ff1f 08fe ff07 faff  ................
        0000050: ffff 0f15 0a09 7069 7169 2d74 7970 6512  ......piqi-type.
        0000060: 0675 696e 7433 3218 0318 0018 ffff ffff  .uint32.........
        0000070: 0ffa ffff ff0f 1b0a 0970 6971 692d 7479  .........piqi-ty
        0000080: 7065 120c 7569 6e74 3332 2d66 6978 6564  pe..uint32-fixed
        0000090: 1804 2500 0000 0025 ffff ffff faff ffff  ..%....%........
        00000a0: 0f14 0a09 7069 7169 2d74 7970 6512 0569  ....piqi-type..i
        00000b0: 6e74 3332 1805 28ff ffff ff0f 28fe ffff  nt32..(.....(...
        00000c0: ff0f faff ffff 0f1a 0a09 7069 7169 2d74  ..........piqi-t
        00000d0: 7970 6512 0b69 6e74 3332 2d66 6978 6564  ype..int32-fixed
        00000e0: 1806 3500 0000 8035 ffff ff7f faff ffff  ..5....5........
        00000f0: 0f1d 0a09 7069 7169 2d74 7970 6512 0e70  ....piqi-type..p
        0000100: 726f 746f 6275 662d 696e 7433 3218 0738  rotobuf-int32..8
        0000110: 8080 8080 f8ff ffff ff01 38ff ffff ff07  ..........8.....
        0000120: faff ffff 0f15 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000130: 6512 0675 696e 7436 3418 0840 0040 ffff  e..uint64..@.@..
        0000140: ffff ffff ffff ff01 faff ffff 0f1b 0a09  ................
        0000150: 7069 7169 2d74 7970 6512 0c75 696e 7436  piqi-type..uint6
        0000160: 342d 6669 7865 6418 0949 0000 0000 0000  4-fixed..I......
        0000170: 0000 49ff ffff ffff ffff fffa ffff ff0f  ..I.............
        0000180: 140a 0970 6971 692d 7479 7065 1205 696e  ...piqi-type..in
        0000190: 7436 3418 0a50 ffff ffff ffff ffff ff01  t64..P..........
        00001a0: 50fe ffff ffff ffff ffff 01fa ffff ff0f  P...............
        00001b0: 1a0a 0970 6971 692d 7479 7065 120b 696e  ...piqi-type..in
        00001c0: 7436 342d 6669 7865 6418 0b59 0000 0000  t64-fixed..Y....
        00001d0: 0000 0080 59ff ffff ffff ffff 7ffa ffff  ....Y...........
        00001e0: ff0f 1d0a 0970 6971 692d 7479 7065 120e  .....piqi-type..
        00001f0: 7072 6f74 6f62 7566 2d69 6e74 3634 180c  protobuf-int64..
        0000200: 6080 8080 8080 8080 8080 0160 ffff ffff  `..........`....
        0000210: ffff ffff 7f                             .....
```



####    float.piq    ####

*   [Source](#float_piq_source)
*   [Piq](#float_piq_piq)
*   [JSON](#float_piq_json)
*   [XML](#float_piq_xml)
*   [Piq (with embedded Piqi)](#float_piq_piq_embedded)
*   [Pib](#float_piq_pib)

<a name="float_piq_source"/>
```
        % floating point values examples
        %
        % NOTE: "float" and "float64" are the same types with different names (IEEE 754
        % double precision).
        %
        (:float)  % all subsequent values have type "float"

        0.0 -10.0

        3.14159

        -2e15
        5.6e-10

        % integer values are converted to floats implicitly
        0

        -100000000000

        0xffff_ffff_ffff_ffff 

        % not a number, positive and negative infinity

        0.nan 0.inf -0.inf

        %
        % IEEE 754 single precision
        %
        (:float32)

        0.0 3.14159 

        2e15
        0.56e-10

        -100000000000

        0xffff_ffff_ffff_ffff

        0.nan 0.inf -0.inf
```

<a name="float_piq_piq"/>
```



        (:float)

        0.0

        -10.0

        3.14159

        -2000000000000000.0

        5.6e-10

        0.0

        -100000000000.0

        1.8446744073709552e+19

        0.nan

        0.inf

        -0.inf

        (:float32)

        0.0

        3.14159

        2000000000000000.0

        5.6e-11

        -100000000000.0

        1.8446744073709552e+19

        0.nan

        0.inf

        -0.inf

```

<a name="float_piq_json"/>


```
        { "piqi_type": "float", "value": 0.0 }

        { "piqi_type": "float", "value": -10.0 }

        { "piqi_type": "float", "value": 3.14159 }

        { "piqi_type": "float", "value": -2000000000000000.0 }

        { "piqi_type": "float", "value": 5.6e-10 }

        { "piqi_type": "float", "value": 0.0 }

        { "piqi_type": "float", "value": -100000000000.0 }

        { "piqi_type": "float", "value": 1.8446744073709552e+19 }

        { "piqi_type": "float", "value": "NaN" }

        { "piqi_type": "float", "value": "Infinity" }

        { "piqi_type": "float", "value": "-Infinity" }

        { "piqi_type": "float32", "value": 0.0 }

        { "piqi_type": "float32", "value": 3.14159 }

        { "piqi_type": "float32", "value": 2000000000000000.0 }

        { "piqi_type": "float32", "value": 5.6e-11 }

        { "piqi_type": "float32", "value": -100000000000.0 }

        { "piqi_type": "float32", "value": 1.8446744073709552e+19 }

        { "piqi_type": "float32", "value": "NaN" }

        { "piqi_type": "float32", "value": "Infinity" }

        { "piqi_type": "float32", "value": "-Infinity" }

```

<a name="float_piq_xml"/>


```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>0.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-10.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>3.14159</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-2000000000000000.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>5.6e-10</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>0.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-100000000000.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>1.8446744073709552e+19</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>NaN</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>Infinity</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-Infinity</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>0.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>3.14159</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>2000000000000000.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>5.6e-11</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-100000000000.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>1.8446744073709552e+19</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>NaN</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>Infinity</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>-Infinity</value>
```


<a name="float_piq_piq_embedded"/>
```

        (:float)

        0.0

        -10.0

        3.14159

        -2000000000000000.0

        5.6e-10

        0.0

        -100000000000.0

        1.8446744073709552e+19

        0.nan

        0.inf

        -0.inf

        (:float32)

        0.0

        3.14159

        2000000000000000.0

        5.6e-11

        -100000000000.0

        1.8446744073709552e+19

        0.nan

        0.inf

        -0.inf
```
<a name="float_piq_pib"/>
```
        0000000: faff ffff 0f14 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0566 6c6f 6174 1801 0900 0000 0000  e..float........
        0000020: 0000 0009 0000 0000 0000 24c0 096e 861b  ..........$..n..
        0000030: f0f9 2109 4009 0000 3426 f56b 1cc3 0903  ..!.@...4&#038;.k....
        0000040: 384a e5cf 3d03 3e09 0000 0000 0000 0000  8J..=.>.........
        0000050: 0900 0000 e876 4837 c209 0000 0000 0000  .....vH7........
        0000060: f043 0901 0000 0000 00f0 7f09 0000 0000  .C..............
        0000070: 0000 f07f 0900 0000 0000 00f0 fffa ffff  ................
        0000080: ff0f 160a 0970 6971 692d 7479 7065 1207  .....piqi-type..
        0000090: 666c 6f61 7433 3218 010d 0000 0000 0dd0  float32.........
        00000a0: 0f49 400d a95f e358 0d65 4a76 2e0d b743  .I@.._.X.eJv...C
        00000b0: bad1 0d00 0080 5f0d 0000 c07f 0d00 0080  ......_.........
        00000c0: 7f0d 0000 80ff                           ......
```




####    string.piq    ####

*   [Source](#string_piq_source)
*   [Piq](#string_piq_piq)
*   [JSON](#string_piq_json)
*   [XML](#string_piq_xml)
*   [Piq (with embedded Piqi)](#string_piq_piq_embedded)
*   [Pib](#string_piq_pib)

<a name="string_piq_source"/>
```

        :string "this is a string\n"

        % "hi" in Russian (utf-8 encoded cyrillic characters)
        :string "привет"

        % these are supported string escape sequences
        :string "\" \t\n\r  \x20 \u0020 \U00000020"

        :string "\x74\x79\x70\x65"

        % NOTE: octal escape codes are unsupported (e.g. "\000\123")

        % binary values must not contain Unicode characters with codes > 127, any ASCII
        % string literal containing ascii-characters represents a valid binary value

        :binary "this is a binary literal"

        :binary "binary literals may contain bytes encoded like this: \xfe"

        :binary "non-unicode escapes are also allowed in binary literals: \" \t\r\n"

        %
        % see also ./piq-text.piq
        %
```
<a name="string_piq_piq"/>
```
        :string "this is a string\n"

        :string "привет"

        :string "\" \t\n\r       "

        :string "type"

        :binary "this is a binary literal"

        :binary "binary literals may contain bytes encoded like this: \xfe"

        :binary "non-unicode escapes are also allowed in binary literals: \" \t\r\n"
```
<a name="string_piq_json"/>
```
        { "piqi_type": "string", "value": "this is a string\n" }

        { "piqi_type": "string", "value": "привет" }

        { "piqi_type": "string", "value": "\" \t\n\r       " }

        { "piqi_type": "string", "value": "type" }

        { "piqi_type": "binary", "value": "dGhpcyBpcyBhIGJpbmFyeSBsaXRlcmFs" }

        {
          "piqi_type": "binary",
          "value":
            "YmluYXJ5IGxpdGVyYWxzIG1heSBjb250YWluIGJ5dGVzIGVuY29kZWQgbGlrZSB0aGlzOiD+"
        }

        {
          "piqi_type": "binary",
          "value":
            "bm9uLXVuaWNvZGUgZXNjYXBlcyBhcmUgYWxzbyBhbGxvd2VkIGluIGJpbmFyeSBsaXRlcmFsczogIiAJDQo="
        }
```
<a name="string_piq_xml"/>
```

        <?xml version="1.0" encoding="UTF-8"?>
        <value>this is a string
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>привет</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>"    

               </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>type</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>dGhpcyBpcyBhIGJpbmFyeSBsaXRlcmFs</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>YmluYXJ5IGxpdGVyYWxzIG1heSBjb250YWluIGJ5dGVzIGVuY29kZWQgbGlrZSB0aGlzOiD+</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>bm9uLXVuaWNvZGUgZXNjYXBlcyBhcmUgYWxzbyBhbGxvd2VkIGluIGJpbmFyeSBsaXRlcmFsczogIiAJDQo=</value>
```
<a name="string_piq_piq_embedded"/>
```
        :string "this is a string\n"

        :string "привет"

        :string "\" \t\n\r       "

        :string "type"

        :binary "this is a binary literal"

        :binary "binary literals may contain bytes encoded like this: \xfe"

        :binary "non-unicode escapes are also allowed in binary literals: \" \t\r\n"
```
<a name="string_piq_pib"/>
```
        0000000: faff ffff 0f15 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0673 7472 696e 6718 0212 1174 6869  e..string....thi
        0000020: 7320 6973 2061 2073 7472 696e 670a 120c  s is a string...
        0000030: d0bf d180 d0b8 d0b2 d0b5 d182 120c 2220  .............." 
        0000040: 090a 0d20 2020 2020 2020 1204 7479 7065  ...       ..type
        0000050: faff ffff 0f15 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000060: 6512 0662 696e 6172 7918 031a 1874 6869  e..binary....thi
        0000070: 7320 6973 2061 2062 696e 6172 7920 6c69  s is a binary li
        0000080: 7465 7261 6c1a 3662 696e 6172 7920 6c69  teral.6binary li
        0000090: 7465 7261 6c73 206d 6179 2063 6f6e 7461  terals may conta
        00000a0: 696e 2062 7974 6573 2065 6e63 6f64 6564  in bytes encoded
        00000b0: 206c 696b 6520 7468 6973 3a20 fe1a 3e6e   like this: ..>n
        00000c0: 6f6e 2d75 6e69 636f 6465 2065 7363 6170  on-unicode escap
        00000d0: 6573 2061 7265 2061 6c73 6f20 616c 6c6f  es are also allo
        00000e0: 7765 6420 696e 2062 696e 6172 7920 6c69  wed in binary li
        00000f0: 7465 7261 6c73 3a20 2220 090d 0a         terals: " ...
```


####    text.piq    ####

*   [Source](#text_piq_source)
*   [Piq](#text_piq_piq)
*   [JSON](#text_piq_json)
*   [XML](#text_piq_xml)
*   [Piq (with embedded Piqi)](#text_piq_piq_embedded)
*   [Pib](#text_piq_pib)

<a name="text_piq_source"/>
```
        (:piq-format/text)

        % text literal are separated between subsequent text literals either by some
        % other lexical element or by empty vertical space

        # single-line verbatim text

        # multi-line verbatim test
        # here's another line
        #
        # and another one
        #

        %
        % whitespace before '#' character is discarded
        %

                # one more line of text

            #
            # that's it

        %
        % verbatim text literals can also be used for representing string values
        %

        :string # text line

        :string
            # text multi
            # line
```
<a name="text_piq_piq"/>
```
        (:piq-format/text)

        # single-line verbatim text

        # multi-line verbatim test
        # here's another line
        #
        # and another one
        #

        # one more line of text

        #
        # that's it

        :string "text line"

        :string "text multi\nline"
```
<a name="text_piq_json"/>
```
        { "piqi_type": "piq-format/text", "value": "single-line verbatim text" }

        {
          "piqi_type": "piq-format/text",
          "value":
            "multi-line verbatim test\nhere's another line\n\nand another one\n"
        }

        { "piqi_type": "piq-format/text", "value": "one more line of text" }

        { "piqi_type": "piq-format/text", "value": "\nthat's it" }

        { "piqi_type": "string", "value": "text line" }

        { "piqi_type": "string", "value": "text multi\nline" }
```
<a name="text_piq_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>single-line verbatim text</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>multi-line verbatim test
        here's another line

        and another one
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>one more line of text</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
        that's it</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>text line</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>text multi
        line</value>
```
<a name="text_piq_piq_embedded"/>
```
        :piqi [
            .module piq-format
            .alias [
                .name word
                .type string
                .piq-format.word
            ]
            .alias [
                .name text
                .type string
                .piq-format.text
            ]
        ]

        (:piq-format/text)

        # single-line verbatim text

        # multi-line verbatim test
        # here's another line
        #
        # and another one
        #

        # one more line of text

        #
        # that's it

        :string "text line"

        :string "text multi\nline"
```
<a name="text_piq_pib"/>
```
        0000000: faff ffff 0f1e 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0f70 6971 2d66 6f72 6d61 742f 7465  e..piq-format/te
        0000020: 7874 1801 0a19 7369 6e67 6c65 2d6c 696e  xt....single-lin
        0000030: 6520 7665 7262 6174 696d 2074 6578 740a  e verbatim text.
        0000040: 3e6d 756c 7469 2d6c 696e 6520 7665 7262  >multi-line verb
        0000050: 6174 696d 2074 6573 740a 6865 7265 2773  atim test.here's
        0000060: 2061 6e6f 7468 6572 206c 696e 650a 0a61   another line..a
        0000070: 6e64 2061 6e6f 7468 6572 206f 6e65 0a0a  nd another one..
        0000080: 156f 6e65 206d 6f72 6520 6c69 6e65 206f  .one more line o
        0000090: 6620 7465 7874 0a0a 0a74 6861 7427 7320  f text...that's 
        00000a0: 6974 faff ffff 0f15 0a09 7069 7169 2d74  it........piqi-t
        00000b0: 7970 6512 0673 7472 696e 6718 0212 0974  ype..string....t
        00000c0: 6578 7420 6c69 6e65 120f 7465 7874 206d  ext line..text m
        00000d0: 756c 7469 0a6c 696e 65                   ulti.line
```

####    any.piq    ####

*   [Source](#any_piq_source)
*   [Piq](#any_piq_piq)
*   [JSON](#any_piq_json)
*   [XML](#any_piq_xml)
*   [Piq (with embedded Piqi)](#any_piq_piq_embedded)
*   [Pib](#any_piq_pib)

<a name="any_piq_source"/>
```
        % this file contains examples of values of the "piqi-any" type; "piqi-any" type
        % represents some typed (piq) or untyped data (piq, json or xml)

        (:piqi-any)  % type hint

        % untyped Piq data

        (.foo)

        1

        "string"

        word

        3.14159

        false

        # verbatim text spanning
        # two lines

        []

        [.foo .bar]

        .foo [ .bar 1 ]

        % typed Piq data

        :int 10

        :float 1.2345

        :string "s"

        :person/person [
            .name "Joe User"
            .id 1
            .phone [ "(555) 123 45 67" .work ]
        ]

        :string # verbatim text

        % untyped JSON (via built-in "json" form)

        (json
            # [{"i": 1}, "foo"]
        )

        (json
            # 1
        )

        (json
            # []
        )

        % untyped XML (via built-in "xml" form)

        (xml
            # <value>
            #   <i>1</i>
            #   <foo/>
            # </value>
        )
```
<a name="any_piq_piq"/>

```
        (:piqi-any)

        .foo

        1

        "string"

        word

        3.14159

        false

        # verbatim text spanning
        # two lines

        []

        [ .foo .bar ]

        .foo [ .bar 1 ]

        :int 10

        :float 1.2345

        :string "s"

        :person/person [
            .name "Joe User"
            .id 1
            .phone [
                .number "(555) 123 45 67"
                .type.work
            ]
        ]

        :string "verbatim text"

        (json 
            # [
            #   {
            #     "i": 1
            #   },
            #   "foo"
            # ]
        )

        (json 
            # 1
        )

        (json 
            # []
        )

        (xml 
            # <value>
            #   <i>1</i>
            #   <foo/>
            # </value>
        )
```
<a name="any_piq_json"/>

```
        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "piqi-any", "value": null }

        { "piqi_type": "int", "value": 10 }

        { "piqi_type": "float", "value": 1.2345 }

        { "piqi_type": "string", "value": "s" }

        {
          "piqi_type": "person/person",
          "name": "Joe User",
          "id": 1,
          "phone": [ { "number": "(555) 123 45 67", "type": "work" } ]
        }

        { "piqi_type": "string", "value": "verbatim text" }

        { "piqi_type": "piqi-any", "value": [ { "i": 1 }, "foo" ] }

        { "piqi_type": "piqi-any", "value": 1 }

        { "piqi_type": "piqi-any", "value": [] }

        { "piqi_type": "piqi-any", "value": null }
```
<a name="any_piq_xml"/>

```

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>10</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>1.2345</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>s</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <name>Joe User</name>
          <id>1</id>
          <phone>
            <number>(555) 123 45 67</number>
            <type>work</type>
          </phone>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>verbatim text</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <i>1</i>
          <foo/>
        </value>
```
<a name="any_piq_piq_embedded"/>
```

        (:piqi-any)

        .foo

        1

        "string"

        word

        3.14159

        false

        # verbatim text spanning
        # two lines

        []

        [ .foo .bar ]

        .foo [ .bar 1 ]

        :int 10

        :float 1.2345

        :string "s"

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
            .name "Joe User"
            .id 1
            .phone [
                .number "(555) 123 45 67"
                .type.work
            ]
        ]

        :string "verbatim text"

        (json 
            # [
            #   {
            #     "i": 1
            #   },
            #   "foo"
            # ]
        )

        (json 
            # 1
        )

        (json 
            # []
        )

        (xml 
            # <value>
            #   <i>1</i>
            #   <foo/>
            # </value>
        )
```        
<a name="any_piq_pib"/>
```
        0000000: faff ffff 0f17 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0870 6971 692d 616e 7918 010a 000a  e..piqi-any.....
        0000020: 000a 000a 000a 000a 000a 000a 000a 000a  ................
        0000030: 00fa ffff ff0f 120a 0970 6971 692d 7479  .........piqi-ty
        0000040: 7065 1203 696e 7418 0210 14fa ffff ff0f  pe..int.........
        0000050: 140a 0970 6971 692d 7479 7065 1205 666c  ...piqi-type..fl
        0000060: 6f61 7418 0319 8d97 6e12 83c0 f33f faff  oat.....n....?..
        0000070: ffff 0f15 0a09 7069 7169 2d74 7970 6512  ......piqi-type.
        0000080: 0673 7472 696e 6718 0422 0173 faff ffff  .string..".s....
        0000090: 0f1c 0a09 7069 7169 2d74 7970 6512 0d70  ....piqi-type..p
        00000a0: 6572 736f 6e2f 7065 7273 6f6e 1805 2a21  erson/person..*!
        00000b0: 0a08 4a6f 6520 5573 6572 1002 2213 0a0f  ..Joe User.."...
        00000c0: 2835 3535 2920 3132 3320 3435 2036 3710  (555) 123 45 67.
        00000d0: 0322 0d76 6572 6261 7469 6d20 7465 7874  .".verbatim text
        00000e0: 0a25 c2a2 889a 031f 5b0a 2020 7b0a 2020  .%......[.  {.  
        00000f0: 2020 2269 223a 2031 0a20 207d 2c0a 2020    "i": 1.  },.  
        0000100: 2266 6f6f 220a 5d0a 07c2 a288 9a03 0131  "foo".]........1
        0000110: 0a08 c2a2 889a 0302 5b5d 0a29 badd ed16  ........[].)....
        0000120: 243c 7661 6c75 653e 0a20 203c 693e 313c  $<value>.  <i>1<
        0000130: 2f69 3e0a 2020 3c66 6f6f 2f3e 0a3c 2f76  /i>.  <foo/>.</v
        0000140: 616c 7565 3e                             alue>
```

###    Addressbook example    ###


                `addressbook.proto` 是对addressbook数据结果的定义.该文件取自[Protocol Buffers 教程](http://protobuf.googlecode.com/svn/trunk/examples/).
        `addressbook.piq`是一个_addressbook_ 实例.

####    addressbook.proto    ####

    *   [Source](#addressbook_proto_source)
    *   [Proto.Piqi](#addressbook_proto_piqi)
    *   [Piqi-light](#addressbook_proto_piqi_light)
    <a name="addressbook_proto_source"/>
```
        // This file was taken from Google Protocol Buffers source distribution. It is
        // also available here:
        //
        //     http://protobuf.googlecode.com/svn/trunk/examples/addressbook.proto

        package tutorial;

        option java_package = "com.example.tutorial";
        option java_outer_classname = "AddressBookProtos";

        message Person {
          required string name = 1;
          required int32 id = 2;        // Unique ID number for this person.
          optional string email = 3;

          enum PhoneType {
            MOBILE = 0;
            HOME = 1;
            WORK = 2;
          }

          message PhoneNumber {
            required string number = 1;
            optional PhoneType type = 2 [default = HOME];
          }

          repeated PhoneNumber phone = 4;
        }

        // Our address book file is just one of these.
        message AddressBook {
          repeated Person person = 1;
        }
```
    <a name="addressbook_proto_piqi"/>

```
        .protobuf-package "tutorial"

        .record [
            .name person
            .field [
                .name name
                .type string
                .code 1
            ]
            .field [
                .name id
                .type protobuf-int32
                .code 2
            ]
            .field [
                .name email
                .type string
                .optional
                .code 3
            ]
            .field [
                .name phone
                .type person-phone-number
                .repeated
                .code 4
            ]
        ]

        .record [
            .name person-phone-number
            .field [
                .name number
                .type string
                .code 1
            ]
            .field [
                .name type
                .type person-phone-type
                .optional
                .default.home
                .code 2
            ]
        ]

        .enum [
            .name person-phone-type
            .option [
                .name mobile
                .code 0
                .protobuf-name "person_mobile"
            ]
            .option [
                .name home
                .code 1
                .protobuf-name "person_home"
            ]
            .option [
                .name work
                .code 2
                .protobuf-name "person_work"
            ]
        ]

        .record [
            .name address-book
            .field [
                .name person
                .type person
                .repeated
                .code 1
            ]
        ]
```        
    <a name="addressbook_proto_piqi_light"/>
```
        type person =
          {
            - name :: string()
            - id :: protobuf-int32()
            ? email :: string()
            * phone :: person-phone-number()
          }

        type person-phone-number =
          {
            - number :: string()
            ? type :: person-phone-type() = .home
          }

        type person-phone-type =
            | mobile
            | home
            | work

        type address-book =
          {
            * person :: person()
          }
```
####    addressbook.piq    ####


    *   [Source](#addressbook_piq_source)
    *   [Piq](#addressbook_piq_piq)
    *   [JSON](#addressbook_piq_json)
    *   [XML](#addressbook_piq_xml)
    *   [Piq (with embedded Piqi)](#addressbook_piq_piq_embedded)
    *   [Pib](#addressbook_piq_pib)
<a name="addressbook_piq_source"/>
```

        :addressbook/address-book [

            .person [
                .name "J. Random Hacker"
                .id 0

                .email "j.r.hacker@example.com"

                .phone [
                    .number "(111) 123 45 67" % phone is "home" by default
                ]

                .phone [
                    .number "(222) 123 45 67"
                    .mobile % NOTE: this is a "shorthand" for .type.mobile
                ]

                .phone [
                    .number "(333) 123 45 67"
                    .work
                ]

                % this is also valid (but not recormmended)
                .phone [ "(444) 123 45 67" .mobile ]
            ]

            % it is possible to omit optional "email" field
            % and repeated "phone" field
            .person [
                .name "Joe User"
                .id 1

                % it is possible to omit optional "email" field
                % and repeated "phone" field
            ]

            % ... or even omit labels for the required fields (not recommended style
            % though)
            .person [ "Joe User Jr" 2 ]

            % or even like that
            .person [
                "Joe User II"
                3
                "joe.user@example.com"
                .phone [ "(444) 123 45 67" ]
                .phone [ "(555) 123 45 67" .work ]
            ]
        ]
```
<a name="addressbook_piq_piq"/>
```
        :addressbook/address-book [
            .person [
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
                .phone [
                    .number "(444) 123 45 67"
                    .type.mobile
                ]
            ]
            .person [
                .name "Joe User"
                .id 1
            ]
            .person [
                .name "Joe User Jr"
                .id 2
            ]
            .person [
                .name "Joe User II"
                .id 3
                .email "joe.user@example.com"
                .phone [ .number "(444) 123 45 67" ]
                .phone [
                    .number "(555) 123 45 67"
                    .type.work
                ]
            ]
        ]
```
<a name="addressbook_piq_json"/>
```
        {
          "piqi_type": "addressbook/address-book",
          "person": [
            {
              "name": "J. Random Hacker",
              "id": 0,
              "email": "j.r.hacker@example.com",
              "phone": [
                { "number": "(111) 123 45 67", "type": "home" },
                { "number": "(222) 123 45 67", "type": "mobile" },
                { "number": "(333) 123 45 67", "type": "work" },
                { "number": "(444) 123 45 67", "type": "mobile" }
              ]
            },
            { "name": "Joe User", "id": 1 },
            { "name": "Joe User Jr", "id": 2 },
            {
              "name": "Joe User II",
              "id": 3,
              "email": "joe.user@example.com",
              "phone": [
                { "number": "(444) 123 45 67", "type": "home" },
                { "number": "(555) 123 45 67", "type": "work" }
              ]
            }
          ]
        }
```
<a name="addressbook_piq_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <person>
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
            <phone>
              <number>(444) 123 45 67</number>
              <type>mobile</type>
            </phone>
          </person>
          <person>
            <name>Joe User</name>
            <id>1</id>
          </person>
          <person>
            <name>Joe User Jr</name>
            <id>2</id>
          </person>
          <person>
            <name>Joe User II</name>
            <id>3</id>
            <email>joe.user@example.com</email>
            <phone>
              <number>(444) 123 45 67</number>
              <type>home</type>
            </phone>
            <phone>
              <number>(555) 123 45 67</number>
              <type>work</type>
            </phone>
          </person>
        </value>

```
<a name="addressbook_piq_piq_embedded"/>
```
        :piqi [
            .module addressbook
            .protobuf-package "tutorial"
            .record [
                .name person
                .field [
                    .name name
                    .type string
                    .code 1
                ]
                .field [
                    .name id
                    .type protobuf-int32
                    .code 2
                ]
                .field [
                    .name email
                    .type string
                    .optional
                    .code 3
                ]
                .field [
                    .name phone
                    .type person-phone-number
                    .repeated
                    .code 4
                ]
            ]
            .record [
                .name person-phone-number
                .field [
                    .name number
                    .type string
                    .code 1
                ]
                .field [
                    .name type
                    .type person-phone-type
                    .optional
                    .default.home
                    .code 2
                ]
            ]
            .enum [
                .name person-phone-type
                .option [
                    .name mobile
                    .protobuf-name "person_mobile"
                    .code 0
                ]
                .option [
                    .name home
                    .protobuf-name "person_home"
                    .code 1
                ]
                .option [
                    .name work
                    .protobuf-name "person_work"
                    .code 2
                ]
            ]
            .record [
                .name address-book
                .field [
                    .name person
                    .type person
                    .repeated
                    .code 1
                ]
            ]
        ]

        :addressbook/address-book [
            .person [
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
                .phone [
                    .number "(444) 123 45 67"
                    .type.mobile
                ]
            ]
            .person [
                .name "Joe User"
                .id 1
            ]
            .person [
                .name "Joe User Jr"
                .id 2
            ]
            .person [
                .name "Joe User II"
                .id 3
                .email "joe.user@example.com"
                .phone [ .number "(444) 123 45 67" ]
                .phone [
                    .number "(555) 123 45 67"
                    .type.work
                ]
            ]
        ]

```
<a name="addressbook_piq_pib"/>
```
        0000000: faff ffff 0f27 0a09 7069 7169 2d74 7970  .....'..piqi-typ
        0000010: 6512 1861 6464 7265 7373 626f 6f6b 2f61  e..addressbook/a
        0000020: 6464 7265 7373 2d62 6f6f 6b18 0212 ee01  ddress-book.....
        0000030: 0a7e 0a10 4a2e 2052 616e 646f 6d20 4861  .~..J. Random Ha
        0000040: 636b 6572 1000 1a16 6a2e 722e 6861 636b  cker....j.r.hack
        0000050: 6572 4065 7861 6d70 6c65 2e63 6f6d 2211  er@example.com".
        0000060: 0a0f 2831 3131 2920 3132 3320 3435 2036  ..(111) 123 45 6
        0000070: 3722 130a 0f28 3232 3229 2031 3233 2034  7"...(222) 123 4
        0000080: 3520 3637 1000 2213 0a0f 2833 3333 2920  5 67.."...(333) 
        0000090: 3132 3320 3435 2036 3710 0222 130a 0f28  123 45 67.."...(
        00000a0: 3434 3429 2031 3233 2034 3520 3637 1000  444) 123 45 67..
        00000b0: 0a0c 0a08 4a6f 6520 5573 6572 1001 0a0f  ....Joe User....
        00000c0: 0a0b 4a6f 6520 5573 6572 204a 7210 020a  ..Joe User Jr...
        00000d0: 4d0a 0b4a 6f65 2055 7365 7220 4949 1003  M..Joe User II..
        00000e0: 1a14 6a6f 652e 7573 6572 4065 7861 6d70  ..joe.user@examp
        00000f0: 6c65 2e63 6f6d 2211 0a0f 2834 3434 2920  le.com"...(444) 
        0000100: 3132 3320 3435 2036 3722 130a 0f28 3535  123 45 67"...(55
        0000110: 3529 2031 3233 2034 3520 3637 1002       5) 123 45 67..
```

###    Person example    ###


                这个例子与前一个类似,但是_person_数据类型是直接在`person.piqi`中定义的,而不是从 `.proto`标准中转换而来.  
        `person.piq` 是_person_ 的一个实例.  



####    person.piq    ####

*   [Source](#person_piq_source)
*   [Proto](#person_piqi_proto)
*   [JSON](#person_piq_json)
*   [XML](#person_piq_xml)
*   [Piqi-light](#person_piqi_light)

<a name="person_piq_source"/>
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
<a name="person_piqi_proto"/>

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
<a name="person_piq_json"/>
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
<a name="person_piq_xml"/>
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
<a name="person_piqi_light"/>
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

####    person.piq    ####

*   [Source](#person_piq_source)
*   [Piq](#person_piq_piq)
*   [JSON](#person_piq_json)
*   [XML](#person_piq_xml)
*   [Piq (with embedded Piqi)](#person_piq_piq_embedded)
*   [Pib](#person_piq_pib)

<a name="person_piq_source"/>
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
<a name="person_piq_piq"/>
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
<a name="person_piq_json"/>
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
<a name="person_piq_xml"/>
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
<a name="person_piq_piq_embedded"/>

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
<a name="person_piq_pib"/>
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

###    用户自定义Piqi数据类型    ###

        `def.piqi` 包含了多种自定义数据类型, 诸如records, variants, enums, lists and aliases. 
        `flag.piq` 和 `list.piq` 是在`def.piqi`定义的多种数据类型的范例.

####    def.piqi    ####


*   [Source](#def_piqi_source)
*   [Piqi.Proto](#def_piqi_proto)
*   [Piqi.JSON](#def_piqi_json)
*   [Piqi.XML](#def_piqi_xml)
*   [Piqi-light](#def_piqi_light)

<a name="def_piqi_source"/>
```

        % this is a record definition
        .record [
            .name r

            % required integer field
            .field [
                .name i
                .type int

                % NOTE: fields are "required" by default; one can specify it explicitly:
                %.required
            ]

            % optional string field
            .field [
                .name s
                .type string
                .optional
            ]

            % optional binary field with default value (NOTE: default values may only be
            % specified for optional fields)
            .field [
                .name b
                .type binary
                .optional
                .default "abc \xff\x00"
            ]

            % repeated floating point field
            .field [
                .name f
                .type float
                .repeated
            ]

            % this is a flag, its presence in the record is meaningful by itself, it
            % doesn't carry any additional value; in fact, the value can be omitted or
            % specified as true or false -- see flag.piq for examples and explanations
            .field [
                .name flag

                % NOTE: flags must be defined as .optional; obviously, .default value
                % doesn't make any sense for flags and thus not allowed
                .optional 
            ]

            % a boolean field
            .field [
                % in this case, the name of the field will be taken as the name of type
                % which is "bool"

                .type bool
                .optional
            ]

            % optional "self"
            .field [
                .name self 
                .type r     % here referencing the record we're defining now
                .optional
            ]

            % another optional filed which references type defined below
            .field [
                % NOTE: if field name and type name are the same, field name may
                % be omitted
                .type v
                .optional
            ]
        ]

        .enum [
            .name e
            .option [ .name a .protobuf-name "e_a" ]
            .option [ .name b ]
            .option [ .name c ]
        ]

        % definition of a variant
        .variant [
            .name v

            .option [
                .name i
                .type int
            ]

            .option [
                % NOTE: if option name and option type are the same, field name may
                % be omitted
                .type r
            ]

            .option [
                .type e
            ]

            % options may not be associated with any types, such options are similar to
            % those used in enums
            .option [
                .name flag
            ]

            % those used in enums
            .option [
                .name l
                .type v-list    % see below
            ]
        ]

        % an alias
        .alias [
            .name a
            .type v
        ]

        % just to give an idea of how it can be used 
        .alias [
            .name uuid
            .type binary
        ]

        .alias [
            .name epoch-seconds
            .type uint64
        ]

        % list of v
        .list [
            % NOTE: "-list" suffix is not mandatory, however it is a style convention
            .name v-list
            .type v
        ]

        % list of built-in type
        .list [
            .name int-list
            .type int
        ]

        .list [
            .name int-list-list
            .type int-list
        ]
```
<a name="def_piqi_proto"/>
```

        message r {
            required sint32 i = 1;
            optional string s = 2;
            optional bytes b = 3 [default = "abc \xff\x00"];
            repeated double f = 4;
            optional bool flag = 5;
            optional bool bool = 6;
            optional r self = 7;
            optional v v = 8;
        }

        enum e {
            e_a = 1;
            b = 2;
            c = 3;
        }

        message v {
            optional sint32 i = 1;
            optional r r = 2;
            optional e e = 3;
            optional bool flag = 4;
            optional v_list l = 5;
        }

        message a {
            optional sint32 i = 1;
            optional r r = 2;
            optional e e = 3;
            optional bool flag = 4;
            optional v_list l = 5;
        }

        message v_list {
            repeated v elem = 1;
        }

        message int_list {
            repeated sint32 elem = 1;
        }

        message int_list_list {
            repeated int_list elem = 1;
        }
```
<a name="def_piqi_json"/>
```
        {
          "piqi_type": "piqi",
          "module": "def",
          "typedef": [
            {
              "record": {
                "name": "r",
                "field": [
                  { "name": "i", "type": "int", "mode": "required" },
                  { "name": "s", "type": "string", "mode": "optional" },
                  {
                    "name": "b",
                    "type": "binary",
                    "mode": "optional",
                    "default": "YWJjIP8A"
                  },
                  { "name": "f", "type": "float", "mode": "repeated" },
                  { "name": "flag", "mode": "optional" },
                  { "type": "bool", "mode": "optional" },
                  { "name": "self", "type": "r", "mode": "optional" },
                  { "type": "v", "mode": "optional" }
                ]
              }
            },
            {
              "enum": {
                "name": "e",
                "option": [
                  { "name": "a", "protobuf_name": "e_a" },
                  { "name": "b" },
                  { "name": "c" }
                ]
              }
            },
            {
              "variant": {
                "name": "v",
                "option": [
                  { "name": "i", "type": "int" },
                  { "type": "r" },
                  { "type": "e" },
                  { "name": "flag" },
                  { "name": "l", "type": "v-list" }
                ]
              }
            },
            { "alias": { "name": "a", "type": "v" } },
            { "alias": { "name": "uuid", "type": "binary" } },
            { "alias": { "name": "epoch-seconds", "type": "uint64" } },
            { "list": { "name": "v-list", "type": "v" } },
            { "list": { "name": "int-list", "type": "int" } },
            { "list": { "name": "int-list-list", "type": "int-list" } }
          ]
        }

```
<a name="def_piqi_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <module>def</module>
          <typedef>
            <record>
              <name>r</name>
              <field>
                <name>i</name>
                <type>int</type>
                <mode>required</mode>
              </field>
              <field>
                <name>s</name>
                <type>string</type>
                <mode>optional</mode>
              </field>
              <field>
                <name>b</name>
                <type>binary</type>
                <mode>optional</mode>
                <default>YWJjIP8A</default>
              </field>
              <field>
                <name>f</name>
                <type>float</type>
                <mode>repeated</mode>
              </field>
              <field>
                <name>flag</name>
                <mode>optional</mode>
              </field>
              <field>
                <type>bool</type>
                <mode>optional</mode>
              </field>
              <field>
                <name>self</name>
                <type>r</type>
                <mode>optional</mode>
              </field>
              <field>
                <type>v</type>
                <mode>optional</mode>
              </field>
            </record>
          </typedef>
          <typedef>
            <enum>
              <name>e</name>
              <option>
                <name>a</name>
                <protobuf-name>e_a</protobuf-name>
              </option>
              <option>
                <name>b</name>
              </option>
              <option>
                <name>c</name>
              </option>
            </enum>
          </typedef>
          <typedef>
            <variant>
              <name>v</name>
              <option>
                <name>i</name>
                <type>int</type>
              </option>
              <option>
                <type>r</type>
              </option>
              <option>
                <type>e</type>
              </option>
              <option>
                <name>flag</name>
              </option>
              <option>
                <name>l</name>
                <type>v-list</type>
              </option>
            </variant>
          </typedef>
          <typedef>
            <alias>
              <name>a</name>
              <type>v</type>
            </alias>
          </typedef>
          <typedef>
            <alias>
              <name>uuid</name>
              <type>binary</type>
            </alias>
          </typedef>
          <typedef>
            <alias>
              <name>epoch-seconds</name>
              <type>uint64</type>
            </alias>
          </typedef>
          <typedef>
            <list>
              <name>v-list</name>
              <type>v</type>
            </list>
          </typedef>
          <typedef>
            <list>
              <name>int-list</name>
              <type>int</type>
            </list>
          </typedef>
          <typedef>
            <list>
              <name>int-list-list</name>
              <type>int-list</type>
            </list>
          </typedef>
        </value>
```
<a name="def_piqi_light"/>
```
        type r =
          {
            - i :: int()
            ? s :: string()
            ? b :: binary() = "abc \xff\x00"
            * f :: float()
            ? flag
            ? bool()
            ? self :: r()
            ? v()
          }

        type e =
            | a
            | b
            | c

        type v =
            | i :: int()
            | r()
            | e()
            | flag
            | l :: v-list()

        type a = v()

        type uuid = binary()

        type epoch-seconds = uint64()

        type v-list = [ v() ]

        type int-list = [ int() ]

        type int-list-list = [ int-list() ]
```
####    flag.piq    ####

*   [Source](#flag_piq_source)
*   [Piq](#flag_piq_piq)
*   [JSON](#flag_piq_json)
*   [XML](#flag_piq_xml)
*   [Piq (with embedded Piqi)](#flag_piq_piq_embedded)
*   [Pib](#flag_piq_pib)

<a name="flag_piq_source"/>
```

        :def/r [
            .i 0
            .flag
        ]

        :def/r [
            .i 0

            % same as .flag
            .flag true
        ]

        :def/r [
            .i 0

            % same as if the flag wasn't present
            .flag false
        ]
```
<a name="flag_piq_piq"/>
```
        :def/r [
            .i 0
            .flag
        ]

        :def/r [
            .i 0
            .flag
        ]

        :def/r [ .i 0 ]
```
<a name="flag_piq_json"/>
```
        { "piqi_type": "def/r", "i": 0, "b": "YWJjIP8A", "flag": true }

        { "piqi_type": "def/r", "i": 0, "b": "YWJjIP8A", "flag": true }

        { "piqi_type": "def/r", "i": 0, "b": "YWJjIP8A" }

```
<a name="flag_piq_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <i>0</i>
          <b>YWJjIP8A</b>
          <flag/>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <i>0</i>
          <b>YWJjIP8A</b>
          <flag/>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <i>0</i>
          <b>YWJjIP8A</b>
        </value>
```
<a name="flag_piq_piq_embedded"/>
```
        :piqi [
            .module def
            .record [
                .name r
                .field [
                    .name i
                    .type int
                ]
                .field [
                    .name s
                    .type string
                    .optional
                ]
                .field [
                    .name b
                    .type binary
                    .optional
                    .default "abc \xff\x00"
                ]
                .field [
                    .name f
                    .type float
                    .repeated
                ]
                .field [
                    .name flag
                    .optional
                ]
                .field [
                    .type bool
                    .optional
                ]
                .field [
                    .name self
                    .type r
                    .optional
                ]
                .field [
                    .type v
                    .optional
                ]
            ]
            .enum [
                .name e
                .option [
                    .name a
                    .protobuf-name "e_a"
                ]
                .option [ .name b ]
                .option [ .name c ]
            ]
            .variant [
                .name v
                .option [
                    .name i
                    .type int
                ]
                .option [ .type r ]
                .option [ .type e ]
                .option [ .name flag ]
                .option [
                    .name l
                    .type v-list
                ]
            ]
            .alias [
                .name a
                .type v
            ]
            .alias [
                .name uuid
                .type binary
            ]
            .alias [
                .name epoch-seconds
                .type uint64
            ]
            .list [
                .name v-list
                .type v
            ]
            .list [
                .name int-list
                .type int
            ]
            .list [
                .name int-list-list
                .type int-list
            ]
        ]

        :def/r [
            .i 0
            .flag
        ]

        :def/r [
            .i 0
            .flag
        ]

        :def/r [ .i 0 ]
```
<a name="flag_piq_pib"/>
```
        0000000: faff ffff 0f14 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0564 6566 2f72 1802 1204 0800 2801  e..def/r......(.
        0000020: 1204 0800 2801 1202 0800                 ....(.....
```


####    list.piq      

*   [Source](#list_piq_source)
*   [Piq](#list_piq_piq)
*   [JSON](#list_piq_json)
*   [XML](#list_piq_xml)
*   [Piq (with embedded Piqi)](#list_piq_piq_embedded)
*   [Pib](#list_piq_pib)   



<a name="list_piq_source"/>
```
        :def/int-list []

        :def/int-list [ 1 2 3 4 5 ]

        :def/int-list-list [
            []
            [ 1 2 3 ]
        ]
```
<a name="list_piq_piq"/>

```
        :def/int-list []

        :def/int-list [ 1 2 3 4 5 ]

        :def/int-list-list [
            []
            [ 1 2 3 ]
        ]
```
<a name="list_piq_json"/>

```
        { "piqi_type": "def/int-list", "value": [] }

        { "piqi_type": "def/int-list", "value": [ 1, 2, 3, 4, 5 ] }

        { "piqi_type": "def/int-list-list", "value": [ [], [ 1, 2, 3 ] ] }
```
<a name="list_piq_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value/>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <item>1</item>
          <item>2</item>
          <item>3</item>
          <item>4</item>
          <item>5</item>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <item/>
          <item>
            <item>1</item>
            <item>2</item>
            <item>3</item>
          </item>
        </value>
```
<a name="list_piq_piq_embedded"/>
```
        :piqi [
            .module def
            .record [
                .name r
                .field [
                    .name i
                    .type int
                ]
                .field [
                    .name s
                    .type string
                    .optional
                ]
                .field [
                    .name b
                    .type binary
                    .optional
                    .default "abc \xff\x00"
                ]
                .field [
                    .name f
                    .type float
                    .repeated
                ]
                .field [
                    .name flag
                    .optional
                ]
                .field [
                    .type bool
                    .optional
                ]
                .field [
                    .name self
                    .type r
                    .optional
                ]
                .field [
                    .type v
                    .optional
                ]
            ]
            .enum [
                .name e
                .option [
                    .name a
                    .protobuf-name "e_a"
                ]
                .option [ .name b ]
                .option [ .name c ]
            ]
            .variant [
                .name v
                .option [
                    .name i
                    .type int
                ]
                .option [ .type r ]
                .option [ .type e ]
                .option [ .name flag ]
                .option [
                    .name l
                    .type v-list
                ]
            ]
            .alias [
                .name a
                .type v
            ]
            .alias [
                .name uuid
                .type binary
            ]
            .alias [
                .name epoch-seconds
                .type uint64
            ]
            .list [
                .name v-list
                .type v
            ]
            .list [
                .name int-list
                .type int
            ]
            .list [
                .name int-list-list
                .type int-list
            ]
        ]

        :def/int-list []

        :def/int-list [ 1 2 3 4 5 ]

        :def/int-list-list [
            []
            [ 1 2 3 ]
        ]
```
<a name="list_piq_pib"/>
```
        0000000: faff ffff 0f1b 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0c64 6566 2f69 6e74 2d6c 6973 7418  e..def/int-list.
        0000020: 0212 0012 0a08 0208 0408 0608 0808 0afa  ................
        0000030: ffff ff0f 200a 0970 6971 692d 7479 7065  .... ..piqi-type
        0000040: 1211 6465 662f 696e 742d 6c69 7374 2d6c  ..def/int-list-l
        0000050: 6973 7418 031a 0a0a 000a 0608 0208 0408  ist.............
        0000060: 06                                       .
```
###    Examples of Piqi functions    ###


        `function.piqi`包括了对Piqi函数定义的范例.  
        `function.piq` 包括了函数定义的输入/输出/错误信息数据类型的范例  

####    function.piqi    ####


*   [Source](#function_piqi_source)
*   [Piqi.Proto](#function_piqi_proto)
*   [Piqi.JSON](#function_piqi_json)
*   [Piqi.XML](#function_piqi_xml)
*   [Piqi-light](#function_piqi_light)

<a name="function_piqi_source"/>
```

        % function with no input and output parameters
        .function [
            .name foo
        ]

        % function with a record input parameter and primitive output and error
        .function [
            .name bar

            .input [
                .field [
                    .type int
                    .optional
                ]
            ]
            .output int
            .error float
        ]

        % function with a record input that has a default value
        .function [
            .name baz

            .input.record [
                .field [
                    .type int
                    .optional
                    .default 10
                ]
            ]
        ]

        % function with a variant input parameter
        .function [
            .name v

            .output.variant [
                .option [
                    .name i
                    .type int
                ]
                .option [
                    .name f
                    .type float
                ]
            ]
        ]

        % function with an enum error parameter
        .function [
            .name e

            .error.enum [
                .option [ .name a ]
                .option [ .name b ]
            ]
        ]

        % function with a list input parameter
        .function [
            .name l

            .input.list [
                .type int
            ]
        ]

        % function with an alias input parameter
        .function [
            .name a

            .input.alias [
                .type string
                .piq-format.text
            ]
        ]
```
<a name="function_piqi_proto"/>
```

        message bar_input {
            optional sint32 int = 1;
        }

        message bar_output {
            required sint32 elem = 1;
        }

        message bar_error {
            required double elem = 1;
        }

        message baz_input {
            optional sint32 int = 1 [default = 10];
        }

        message v_output {
            optional sint32 i = 1;
            optional double f = 2;
        }

        message e_error {
            enum e_error {
                a = 1;
                b = 2;
            };
            required e_error elem = 1;
        }

        message l_input {
            repeated sint32 elem = 1;
        }

        message a_input {
            required string elem = 1;
        }
```
<a name="function_piqi_json"/>

```
        {
          "piqi_type": "piqi",
          "module": "function",
          "typedef": [
            {
              "record": {
                "name": "bar-input",
                "field": [ { "type": "int", "mode": "optional" } ]
              }
            },
            { "alias": { "name": "bar-output", "type": "int" } },
            { "alias": { "name": "bar-error", "type": "float" } },
            {
              "record": {
                "name": "baz-input",
                "field": [ { "type": "int", "mode": "optional", "default": 10 } ]
              }
            },
            {
              "variant": {
                "name": "v-output",
                "option": [
                  { "name": "i", "type": "int" },
                  { "name": "f", "type": "float" }
                ]
              }
            },
            {
              "enum": {
                "name": "e-error",
                "option": [ { "name": "a" }, { "name": "b" } ]
              }
            },
            { "list": { "name": "l-input", "type": "int" } },
            {
              "alias": {
                "name": "a-input",
                "type": "string",
                "piq_format": { "text": true }
              }
            }
          ],
          "function": [
            { "name": "foo" },
            {
              "name": "bar",
              "input": "bar-input",
              "output": "int",
              "error": "float"
            },
            { "name": "baz", "input": "baz-input" },
            { "name": "v", "output": "v-output" },
            { "name": "e", "error": "e-error" },
            { "name": "l", "input": "l-input" },
            { "name": "a", "input": "a-input" }
          ]
        }
```
<a name="function_piqi_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <module>function</module>
          <typedef>
            <record>
              <name>bar-input</name>
              <field>
                <type>int</type>
                <mode>optional</mode>
              </field>
            </record>
          </typedef>
          <typedef>
            <alias>
              <name>bar-output</name>
              <type>int</type>
            </alias>
          </typedef>
          <typedef>
            <alias>
              <name>bar-error</name>
              <type>float</type>
            </alias>
          </typedef>
          <typedef>
            <record>
              <name>baz-input</name>
              <field>
                <type>int</type>
                <mode>optional</mode>
                <default>10</default>
              </field>
            </record>
          </typedef>
          <typedef>
            <variant>
              <name>v-output</name>
              <option>
                <name>i</name>
                <type>int</type>
              </option>
              <option>
                <name>f</name>
                <type>float</type>
              </option>
            </variant>
          </typedef>
          <typedef>
            <enum>
              <name>e-error</name>
              <option>
                <name>a</name>
              </option>
              <option>
                <name>b</name>
              </option>
            </enum>
          </typedef>
          <typedef>
            <list>
              <name>l-input</name>
              <type>int</type>
            </list>
          </typedef>
          <typedef>
            <alias>
              <name>a-input</name>
              <type>string</type>
              <piq-format>
                <text/>
              </piq-format>
            </alias>
          </typedef>
          <function>
            <name>foo</name>
          </function>
          <function>
            <name>bar</name>
            <input>bar-input</input>
            <output>int</output>
            <error>float</error>
          </function>
          <function>
            <name>baz</name>
            <input>baz-input</input>
          </function>
          <function>
            <name>v</name>
            <output>v-output</output>
          </function>
          <function>
            <name>e</name>
            <error>e-error</error>
          </function>
          <function>
            <name>l</name>
            <input>l-input</input>
          </function>
          <function>
            <name>a</name>
            <input>a-input</input>
          </function>
        </value>
```
<a name="function_piqi_light"/>
```
        function foo

        function bar
            input =
              {
                ? int()
              }
            output = int()
            error = float()

        function baz
            input =
              {
                ? int() = 10
              }

        function v
            output =
                | i :: int()
                | f :: float()

        function e
            error =
                | a
                | b

        function l
            input = [ int() ]

        function a
            input = string()
```
####    function.piq    ####

*   [Source](#function_piq_source)
*   [Piq](#function_piq_piq)
*   [JSON](#function_piq_json)
*   [XML](#function_piq_xml)
*   [Piq (with embedded Piqi)](#function_piq_piq_embedded)
*   [Pib](#function_piq_pib)

<a name="function_piq_source"/>
```
        % input/ouput/error of functions defined in function.piqi

        :function/bar-input [ 10 ]
        :function/bar-output 1
        :function/bar-error 100.0

        :function/baz-input []

        :function/v-output.i 0
        :function/v-output.f 100.0

        :function/e-error.a
        :function/e-error.b

        :function/l-input [1 2 3]

        :function/a-input # foo
```
<a name="function_piq_piq"/>
```
        :function/bar-input [ .int 10 ]

        :function/bar-output 1

        :function/bar-error 100.0

        :function/baz-input []

        :function/v-output.i 0

        :function/v-output.f 100.0

        :function/e-error.a

        :function/e-error.b

        :function/l-input [ 1 2 3 ]

        :function/a-input # foo
```
<a name="function_piq_json"/>
```
        { "piqi_type": "function/bar-input", "int": 10 }

        { "piqi_type": "function/bar-output", "value": 1 }

        { "piqi_type": "function/bar-error", "value": 100.0 }

        { "piqi_type": "function/baz-input", "int": 10 }

        { "piqi_type": "function/v-output", "i": 0 }

        { "piqi_type": "function/v-output", "f": 100.0 }

        { "piqi_type": "function/e-error", "value": "a" }

        { "piqi_type": "function/e-error", "value": "b" }

        { "piqi_type": "function/l-input", "value": [ 1, 2, 3 ] }

        { "piqi_type": "function/a-input", "value": "foo" }
```
<a name="function_piq_xml"/>

```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <int>10</int>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>1</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>100.0</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <int>10</int>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <i>0</i>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <f>100.0</f>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>a</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>b</value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <item>1</item>
          <item>2</item>
          <item>3</item>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>foo</value>

```
<a name="function_piq_piq_embedded"/>
```
        :piqi [
            .module function
            .function [ .name foo ]
            .function [
                .name bar
                .input [
                    .field [
                        .type int
                        .optional
                    ]
                ]
                .output int
                .error float
            ]
            .function [
                .name baz
                .input [
                    .field [
                        .type int
                        .optional
                        .default 10
                    ]
                ]
            ]
            .function [
                .name v
                .output.variant [
                    .option [
                        .name i
                        .type int
                    ]
                    .option [
                        .name f
                        .type float
                    ]
                ]
            ]
            .function [
                .name e
                .error.enum [
                    .option [ .name a ]
                    .option [ .name b ]
                ]
            ]
            .function [
                .name l
                .input.list [ .type int ]
            ]
            .function [
                .name a
                .input.alias [
                    .type string
                    .piq-format.text
                ]
            ]
        ]

        :function/bar-input [ .int 10 ]

        :function/bar-output 1

        :function/bar-error 100.0

        :function/baz-input []

        :function/v-output.i 0

        :function/v-output.f 100.0

        :function/e-error.a

        :function/e-error.b

        :function/l-input [ 1 2 3 ]

        :function/a-input # foo
```
<a name="function_piq_pib"/>
```
        0000000: faff ffff 0f21 0a09 7069 7169 2d74 7970  .....!..piqi-typ
        0000010: 6512 1266 756e 6374 696f 6e2f 6261 722d  e..function/bar-
        0000020: 696e 7075 7418 0212 0208 14fa ffff ff0f  input...........
        0000030: 220a 0970 6971 692d 7479 7065 1213 6675  "..piqi-type..fu
        0000040: 6e63 7469 6f6e 2f62 6172 2d6f 7574 7075  nction/bar-outpu
        0000050: 7418 0318 02fa ffff ff0f 210a 0970 6971  t.........!..piq
        0000060: 692d 7479 7065 1212 6675 6e63 7469 6f6e  i-type..function
        0000070: 2f62 6172 2d65 7272 6f72 1804 2100 0000  /bar-error..!...
        0000080: 0000 0059 40fa ffff ff0f 210a 0970 6971  ...Y@.....!..piq
        0000090: 692d 7479 7065 1212 6675 6e63 7469 6f6e  i-type..function
        00000a0: 2f62 617a 2d69 6e70 7574 1805 2a00 faff  /baz-input..*...
        00000b0: ffff 0f20 0a09 7069 7169 2d74 7970 6512  ... ..piqi-type.
        00000c0: 1166 756e 6374 696f 6e2f 762d 6f75 7470  .function/v-outp
        00000d0: 7574 1806 3202 0800 3209 1100 0000 0000  ut..2...2.......
        00000e0: 0059 40fa ffff ff0f 1f0a 0970 6971 692d  .Y@........piqi-
        00000f0: 7479 7065 1210 6675 6e63 7469 6f6e 2f65  type..function/e
        0000100: 2d65 7272 6f72 1807 3801 3802 faff ffff  -error..8.8.....
        0000110: 0f1f 0a09 7069 7169 2d74 7970 6512 1066  ....piqi-type..f
        0000120: 756e 6374 696f 6e2f 6c2d 696e 7075 7418  unction/l-input.
        0000130: 0842 0608 0208 0408 06fa ffff ff0f 1f0a  .B..............
        0000140: 0970 6971 692d 7479 7065 1210 6675 6e63  .piqi-type..func
        0000150: 7469 6f6e 2f61 2d69 6e70 7574 1809 4a03  tion/a-input..J.
        0000160: 666f 6f                                  foo
```
###    Complex numbers    ###


                `complex.piqi` contains definition of a record for representing complex numbers and, together with `complex.piq`, demonstrates the ability to define compound default values for optional fields.
####    complex.piqi    ####


*   [Source](#complex_piqi_source)
*   [Piqi.Proto](#complex_piqi_proto)
*   [Piqi.JSON](#complex_piqi_json)
*   [Piqi.XML](#complex_piqi_xml)
*   [Piqi-light](#complex_piqi_light)

<a name="complex_piqi_source"/>
```

        % a handy type abbreviation
        .alias [
            .name t
            .type complex
        ]

        % complex number
        .record [
            .name complex

            .field [ .name re .type float ]
            .field [ .name im .type float ]
        ]

        % some record which uses "complex" type
        .record [
            .name foo
            .field [
                .name bar
                .type t
                .optional

                % piqi supports structured defaults for optional fields:
                .default [.re 1 .im 0] % NOTE: it is possible to skip names and use [1 0]
            ]
        ]
```
<a name="complex_piqi_proto"/>
```


        message t {
            required double re = 1;
            required double im = 2;
        }

        message complex {
            required double re = 1;
            required double im = 2;
        }

        message foo {
            optional complex bar = 1;
        }
```
<a name="complex_piqi_json"/>
```
        {
          "piqi_type": "piqi",
          "module": "complex",
          "typedef": [
            { "alias": { "name": "t", "type": "complex" } },
            {
              "record": {
                "name": "complex",
                "field": [
                  { "name": "re", "type": "float", "mode": "required" },
                  { "name": "im", "type": "float", "mode": "required" }
                ]
              }
            },
            {
              "record": {
                "name": "foo",
                "field": [
                  {
                    "name": "bar",
                    "type": "t",
                    "mode": "optional",
                    "default": { "re": 1.0, "im": 0.0 }
                  }
                ]
              }
            }
          ]
        }
```
<a name="complex_piqi_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <module>complex</module>
          <typedef>
            <alias>
              <name>t</name>
              <type>complex</type>
            </alias>
          </typedef>
          <typedef>
            <record>
              <name>complex</name>
              <field>
                <name>re</name>
                <type>float</type>
                <mode>required</mode>
              </field>
              <field>
                <name>im</name>
                <type>float</type>
                <mode>required</mode>
              </field>
            </record>
          </typedef>
          <typedef>
            <record>
              <name>foo</name>
              <field>
                <name>bar</name>
                <type>t</type>
                <mode>optional</mode>
                <default>
                  <re>1.0</re>
                  <im>0.0</im>
                </default>
              </field>
            </record>
          </typedef>
        </value>

```
<a name="complex_piqi_light"/>
```
        type t = complex()

        type complex =
          {
            - re :: float()
            - im :: float()
          }

        type foo =
          {
            ? bar :: t() =
                [
                    .re 1
                    .im 0
                ]
          }
```
####    complex.piq    ####

*   [Source](#complex_piq_source)
*   [Piq](#complex_piq_piq)
*   [JSON](#complex_piq_json)
*   [XML](#complex_piq_xml)
*   [Piq (with embedded Piqi)](#complex_piq_piq_embedded)
*   [Pib](#complex_piq_pib)

<a name="complex_piq_source"/>
```
        :complex/t [ .re 0 .im 0 ]

        % field names are optional:
        :complex/t [ 0 0 ]

        % an object without any fields
        :complex/foo []
```
<a name="complex_piq_piq"/>

```
        :complex/t [
            .re 0.0
            .im 0.0
        ]

        :complex/t [
            .re 0.0
            .im 0.0
        ]

        :complex/foo []
```
<a name="complex_piq_json"/>

```
        { "piqi_type": "complex/t", "re": 0.0, "im": 0.0 }

        { "piqi_type": "complex/t", "re": 0.0, "im": 0.0 }

        { "piqi_type": "complex/foo", "bar": { "re": 1.0, "im": 0.0 } }
```
<a name="complex_piq_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <re>0.0</re>
          <im>0.0</im>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <re>0.0</re>
          <im>0.0</im>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <bar>
            <re>1.0</re>
            <im>0.0</im>
          </bar>
        </value>

```
<a name="complex_piq_piq_embedded"/>

```
        :piqi [
            .module complex
            .alias [
                .name t
                .type complex
            ]
            .record [
                .name complex
                .field [
                    .name re
                    .type float
                ]
                .field [
                    .name im
                    .type float
                ]
            ]
            .record [
                .name foo
                .field [
                    .name bar
                    .type t
                    .optional
                    .default [
                        .re 1
                        .im 0
                    ]
                ]
            ]
        ]

        :complex/t [
            .re 0.0
            .im 0.0
        ]

        :complex/t [
            .re 0.0
            .im 0.0
        ]

        :complex/foo []

```

<a name="complex_piq_pib"/>
```
        0000000: faff ffff 0f18 0a09 7069 7169 2d74 7970  ........piqi-typ
        0000010: 6512 0963 6f6d 706c 6578 2f74 1802 1212  e..complex/t....
        0000020: 0900 0000 0000 0000 0011 0000 0000 0000  ................
        0000030: 0000 1212 0900 0000 0000 0000 0011 0000  ................
        0000040: 0000 0000 0000 faff ffff 0f1a 0a09 7069  ..............pi
        0000050: 7169 2d74 7970 6512 0b63 6f6d 706c 6578  qi-type..complex
        0000060: 2f66 6f6f 1803 1a00                      /foo....
```

###    List of variant == record    ###

       

                This example shows relationship between _list of variant_ and _record_ types. Representation of their values in Piq can be the same. Note JSON and binary representation being different.

####    record-variant-list.piqi    ####


*   [Source](#record-variant-list_piqi_source)
*   [Piqi.Proto](#record-variant-list_piqi_proto)
*   [Piqi.JSON](#record-variant-list_piqi_json)
*   [Piqi.XML](#record-variant-list_piqi_xml)
*   [Piqi-light](#record-variant-list_piqi_light)

<a name="record-variant-list_piqi_source"/>
```


        .record [
            .name r
            .field [ .name a .type int ]
            .field [ .name b .type int ]
        ]

        .variant [
            .name v
            .option [ .name a .type int ]
            .option [ .name b .type int ]
        ]

        .list [ .name l .type v ]
```
<a name="record-variant-list_piqi_proto"/>
```
        message r {
            required sint32 a = 1;
            required sint32 b = 2;
        }

        message v {
            optional sint32 a = 1;
            optional sint32 b = 2;
        }

        message l {
            repeated v elem = 1;
        }
```
<a name="record-variant-list_piqi_json"/>
```
        {
          "piqi_type": "piqi",
          "module": "record-variant-list",
          "typedef": [
            {
              "record": {
                "name": "r",
                "field": [
                  { "name": "a", "type": "int", "mode": "required" },
                  { "name": "b", "type": "int", "mode": "required" }
                ]
              }
            },
            {
              "variant": {
                "name": "v",
                "option": [
                  { "name": "a", "type": "int" },
                  { "name": "b", "type": "int" }
                ]
              }
            },
            { "list": { "name": "l", "type": "v" } }
          ]
        }
```
<a name="record-variant-list_piqi_xml"/>
```

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <module>record-variant-list</module>
          <typedef>
            <record>
              <name>r</name>
              <field>
                <name>a</name>
                <type>int</type>
                <mode>required</mode>
              </field>
              <field>
                <name>b</name>
                <type>int</type>
                <mode>required</mode>
              </field>
            </record>
          </typedef>
          <typedef>
            <variant>
              <name>v</name>
              <option>
                <name>a</name>
                <type>int</type>
              </option>
              <option>
                <name>b</name>
                <type>int</type>
              </option>
            </variant>
          </typedef>
          <typedef>
            <list>
              <name>l</name>
              <type>v</type>
            </list>
          </typedef>
        </value>

```
<a name="record-variant-list_piqi_light"/>
```
        type r =
          {
            - a :: int()
            - b :: int()
          }

        type v =
            | a :: int()
            | b :: int()

        type l = [ v() ]
```
####    record-variant-list.piq    ####

*   [Source](#record-variant-list_piq_source)
*   [Piq](#record-variant-list_piq_piq)
*   [JSON](#record-variant-list_piq_json)
*   [XML](#record-variant-list_piq_xml)
*   [Piq (with embedded Piqi)](#record-variant-list_piq_piq_embedded)
*   [Pib](#record-variant-list_piq_pib)

<a name="record-variant-list_piq_source"/>
```
        % record
        :record-variant-list/r [ .a 0 .b 1 ]

        % variant list
        :record-variant-list/l [ .a 0 .b 1 ]

        % abbreviated representation of variant values
        :record-variant-list/v.a 0
        :record-variant-list/v.b 1

        % un-abbreviated representation of variant values
        :record-variant-list/v (.a 0)
        :record-variant-list/v (.b 1)
```
<a name="record-variant-list_piq_piq"/>

```
        :record-variant-list/r [
            .a 0
            .b 1
        ]

        :record-variant-list/l [
            .a 0
            .b 1
        ]

        :record-variant-list/v.a 0

        :record-variant-list/v.b 1

        :record-variant-list/v.a 0

        :record-variant-list/v.b 1
```
<a name="record-variant-list_piq_json"/>
```
        { "piqi_type": "record-variant-list/r", "a": 0, "b": 1 }

        { "piqi_type": "record-variant-list/l", "value": [ { "a": 0 }, { "b": 1 } ] }

        { "piqi_type": "record-variant-list/v", "a": 0 }

        { "piqi_type": "record-variant-list/v", "b": 1 }

        { "piqi_type": "record-variant-list/v", "a": 0 }

        { "piqi_type": "record-variant-list/v", "b": 1 }
```
<a name="record-variant-list_piq_xml"/>
```
        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <a>0</a>
          <b>1</b>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <item>
            <a>0</a>
          </item>
          <item>
            <b>1</b>
          </item>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <a>0</a>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <b>1</b>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <a>0</a>
        </value>

        <?xml version="1.0" encoding="UTF-8"?>
        <value>
          <b>1</b>
        </value>
```
<a name="record-variant-list_piq_piq_embedded"/>
```
        :piqi [
            .module record-variant-list
            .record [
                .name r
                .field [
                    .name a
                    .type int
                ]
                .field [
                    .name b
                    .type int
                ]
            ]
            .variant [
                .name v
                .option [
                    .name a
                    .type int
                ]
                .option [
                    .name b
                    .type int
                ]
            ]
            .list [
                .name l
                .type v
            ]
        ]

        :record-variant-list/r [
            .a 0
            .b 1
        ]

        :record-variant-list/l [
            .a 0
            .b 1
        ]

        :record-variant-list/v.a 0

        :record-variant-list/v.b 1

        :record-variant-list/v.a 0

        :record-variant-list/v.b 1
```
<a name="record-variant-list_piq_pib"/>

```

    0000000: faff ffff 0f24 0a09 7069 7169 2d74 7970  .....$..piqi-typ
    0000010: 6512 1572 6563 6f72 642d 7661 7269 616e  e..record-varian
    0000020: 742d 6c69 7374 2f72 1802 1204 0800 1002  t-list/r........
    0000030: faff ffff 0f24 0a09 7069 7169 2d74 7970  .....$..piqi-typ
    0000040: 6512 1572 6563 6f72 642d 7661 7269 616e  e..record-varian
    0000050: 742d 6c69 7374 2f6c 1803 1a08 0a02 0800  t-list/l........
    0000060: 0a02 1002 faff ffff 0f24 0a09 7069 7169  .........$..piqi
    0000070: 2d74 7970 6512 1572 6563 6f72 642d 7661  -type..record-va
    0000080: 7269 616e 742d 6c69 7374 2f76 1804 2202  riant-list/v..".
    0000090: 0800 2202 1002 2202 0800 2202 1002       .."..."..."...

```

##  OCaml examples  

OCaml 实例 [请查看](/doc/OCaml/#examples).  

##  Erlang examples  

Eralng 实例 [请查看](/doc/erlang/#examples).  

##  Piqi-RPC examples  
Piqi-RPC实例 [请查看](/doc/piqi-rpc/#examples).  
</div>
                                                                                最后一次修订时间: March 30, 2014

  <script src="http://code.jquery.com/jquery-1.9.1.js"></script>
  <script src="http://code.jquery.com/ui/1.10.3/jquery-ui.js"></script>                                                                                
    <script type="text/javascript">
        $(document).ready(function(){

            // accordion
            $('.accordion').accordion({
                header: '.accordion-header',
                autoHeight: false,
                navigation: true,
                collapsible: true,
                active: false
            });

            // accordion
            $('.accordion-homepage').accordion({
                header: '.accordion-header',
                autoHeight: false,
                navigation: true,
                collapsible: true,
                active: 1
            });

            // tabs
            $('.tabs').tabs();
        });
    </script>
