***

<u><b>Intro</b></u>
...

***

<u><b>Macros & Enums</b></u>
* `#macro U64 18446744073709551615
* `#macro U32 4294967295`
* `#macro U16 65535`
* `#macro U8  255`
* `#macro BYTE_MAX 255``

* `enum Locality {
	`Unknown,`
	`Solo,`
	`Local,`
	`Global`
	`}

***

<u><b>Type Definitions</b></u>
* `@typedef {int} int32
* `@typedef {int} bitflag
* `@typedef {int} byte
* `@typedef {int} headertypeindex
* `@typedef {function<bufferIncoming:buffer;void>} headerCommand
* `@typedef {headerCommand} headerReadCommand
* `@typedef {headerCommand} headerWriteCommand

***

<u><b>Global Variables</b></u>
* `headerList` : `Array<Header>` ➡ Array containing all Headers.

***

<u><b>Static Variables</b></u>
...

***

<u><b>Constructor Parameters</b></u>
* `_bufferType` : `buffer_type`
* `_flagsValueMax` : `int`
* `_flagCount` : `int`
* `_locality` : `Locality`

***

<u><b>Instance Variables</b></u>
...

***