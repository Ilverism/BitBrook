***

<u><b>Intro</b></u>

The #Header is used to ...

***

<u><b>Default Child Classes</b></u>

The following child classes are used to define the maximum number of bit flags a Header may contain. Using a Header with a larger number of flags will increase the number of different possible updates that can be defined at the expense of an increase in packet size.
* Header_8
* Header_16
* Header_32
* Header_64

***

<u><b>Macros & Enums</b></u>
* `#macro U64 18446744073709551615
* `#macro U32 4294967295`
* `#macro U16 65535`
* `#macro U8  255`
* `#macro BYTE_MAX 255

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
* 🟡 `_bufferType` : `buffer_type`
* 🟢 `_flagsValueMax` : `int`
* 🟣 `_flagCount` : `int`
* 🔵 `_locality` : `Locality`

***

<u><b>Instance Variables</b></u>

* 🟡 `bufferType` : `buffer_type`
* `flags = 0b0` : `bitflag`
* 🟢 `flagsValueMax` : `int`
* 🟣 `flagCount` : `int`
* 🔵 `locality [=Locality.Unknown]` : `Locality`
* `headerReadCommands` : `array<headerReadCommand>`
* `headerWriteCommands` : `array<headerWriteCommand>`
* `subheaders` : `array<Header>`

***

<u><b>Static Methods</b></u>

#### Read/Write Commands

###### Preflag Commands

❗ Preflag commands are executed unconditionally before the Header builds or reads any data.

<u>header_preflag_write</u> (Abstract)
* Description
	* Aa.
* Parameters
	* `bufferOut` : `buffer`
	* `[...rest]` : `any`

<u>header_preflag_read</u> (Abstract)
* Description
	* Aa.
	* ❗ If this returns `false`, the `parse_incoming` method which calls this will discard all other incoming data not already handled.
* Parameters
	* `bufferOut` : `buffer`
	* `[...rest]` : `any`
 * Return : `bool`

###### Read Commands

<u>header_read_command_add</u>
* Description
	* Aa.
* Parameters
	* `flagDataKey` : `int`
	* `dataMethod` : `headerReadCommand`

<u>header_read_command_fetch</u>
* Description
	* Aa.
* Parameters
	* `flagDataKey` : `int`
* Return : `headerReadCommand`

<u>header_read_command_fetch_index</u>
* Description
	* Aa.
* Parameters
	* `flagDataKeyIndex` : `int`
* Return : `headerReadCommand`

###### Write Commands

<u>header_write_command_add</u>
* Description
	* Aa.
* Parameters
	* `flagDataKey` : `int`
	* `dataMethod` : `headerWriteCommand`

<u>header_write_command_fetch</u>
* Description
	* Aa.
* Parameters
	* `flagDataKey` : `int`
* Return : `headerWriteCommand`

<u>header_write_command_fetch_index</u>
* Description
	* Aa.
* Parameters
	* `flagDataKeyIndex` : `int`
* Return : `headerWriteCommand`

<u>header_write_command_execute</u>
* Description
	* Aa.
* Parameters
	* `flagDataKey` : `int`
	* `[...rest]` : `any`

<u>header_write_command_execute_index</u>
* Description
	* Aa.
* Parameters
	* `flagDataKeyIndex` : `int`
	* `[...rest]` : `int`

#### Getters

<u>get_header_consecutor</u>
* Description
	* Gets the #Consecutor corresponding to this Header's type index.
* Return : `Consecutor`

<u>has_flag</u>
* Description
	* Returns `true` if any bit flags have been set, `false` otherwise.
* Return : `bool`

<u>is_empty</u>
* Description
	* Returns `false` if any bit flags have been set, `true` otherwise (inverse of `has_flag`).
* Return : `bool`

<u>is_marked</u>
* Description
	* Returns whether or not a specific bit has been flagged.
* Parameters
	* `n` : `bitflag
* Return : `bool`

<u>is_exceeded</u>
* Description
	* For debugging purposes
	* Returns whether or not the total value of the currently set flags exceeds the maximum possible flags value.
* Return : `bool`
#### Other

<u>write</u>
* Description
	* Writes this Header's flags to the target buffer and then clears all flags.
* Parameters
	* `bufferTarget` : `buffer

<u>clear</u>
* Description
	* Clears all flags to `0`.

<u>mark</u>
* Description
	* Marks one or more bit flags based on the input as `1`.
* Parameters
	* `bitFlagsIn` : `bitflag`

<u>parse_incoming</u>
* Description
	* Handles an incoming buffer containing data compatible with this Header.
	* ❗ Will call the `header_preflag_read` method before handling other flagged commands. However, if the method returns `false`, all other data in the buffer will be discarded instead.
* Parameters
	* `bitFlagsIn` : `bitflag`

***
