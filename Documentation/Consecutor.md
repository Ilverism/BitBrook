***

<u><b>Intro</b></u>

The #Consecutor is used to stream multiple instances of the same type of #Header data in a single packet. The already-compressed header buffers are consecutively passed to a Consecutor instance and rebuilt into a single, further-compressed buffer.

The reliability of the packet being output is tied to a value provided to the Consecutor when it is created, so Consecutors handling Headers with critical data should use <i>steam_net_packet_type_reliable</i> instead of the default <i>steam_net_packet_type_unreliable</i> value.
Furthermore, this also means that multiple Headers handling similar data may need to be split into 2 different instances if some of that data is critical while part of it is not. If this is the case, 2 different Consecutors will need to be created to match those Headers.

<i>Example:</i>

Suppose a 'Unit' instance in a game has flags for 'Position' and 'Item' data updates, and the given Unit's position is constantly being updated while their items are not. Then, the Position data can be considered a non-critical piece of data that can be sent unreliably, while the Item data can be considered critical and must be sent reliably.
Here, we require 2 different Headers. We can call these 'Header_Unit' (for unreliable data) and 'Header_UnitCritical' (for reliable data). The ...

***

<u><b>Default Child Classes</b></u>
None.

***

<u><b>Macros & Enums</b></u>
None.

****

<u><b>Type Definitions</b></u>
None.

***

<u><b>Global Variables</b></u>

* `consecutorTypeMap` : `array<Consecutor>` ➡ Array containing all Consecutors. When a Consecutor is initialized, it is recorded in this array with its index being its `headerTypeIndexTarget` value, which is determined by the Consecutor's corresponding Header.

****

<u><b>Static Variables</b></u>
None.

****

<u><b>Constructor Parameters</b></u>
* 🟡 `_headerType` : `Header`
* 🟢 `_packetReliabilityType [=steam_net_packet_type_unreliable]`

****

<u><b>Instance Variables</b></u>
* 🟡 `headerTypeIndexTarget` : `headertypeindex` ➡ Refers to the runtime constant index for the type of #Header to compress.
* 🟢 `packetReliabilityType` ➡ Reliability of the packet to output.

***

<u><b>Static Methods</b></u>

<u>build</u>
* Description
	* Takes an array of Headers as input. The Headers sequentially produce their individual buffers, which are then added to a new output buffer and then deleted. This buffer is returned when complete.
* Parameters
	* `headersIn` : `array<Header>`
* Return : `buffer`

<u>build_compressed</u>
* Description
	* Takes an array of Headers as input. Calls the <u>build</u> method on the provided array of Headers, and outputs a compressed copy of the returned buffer. The uncompressed version is deleted.
* Parameters 
	* `headersIn` : `array<Header>`
* Return : `buffer_compressed`

***

<u><b>Global Script Functions</b></u>

<u>get_consecutor</u>
* Description
	* Returns a Consecutor from the global
* Parameters
	* `headerTypeIndexTarget` : `headertypeindex`
* Return : `Consecutor`