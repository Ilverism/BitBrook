***

<u><b>Intro</b></u>

The #Brook is used to hold an array of buffers which each correspond to relevant #Header flags.

This results in the dat being broadcast and received in the order specified by the Header flag enumerators, regardless of the order the data buffers were constructed.

When the data is ready to be exported, the user may construct the compiled data normally with the `build` method, or create a compressed version with the `build_compressed` method (recommended). While these methods may be called directly on the Brook instances for use in certain cases (e.g. when only a single chunk of buffered data needs to be exported), it is more likely that the #Consecutor version of these methods should be used instead.

(Brooks instances are not used for reading incoming data, only writing and uploading it.)

***

<u><b>Default Child Classes</b></u>
None.

***

<u><b>Macros & Enums</b></u>
* `#macro BROOK_BUFFER_UNSET -1`

***

<u><b>Type Definitions</b></u>
* `@typedef {number} brook_buffer_unset`

***

<u><b>Global Variables</b></u>
None.

***

<u><b>Static Variables</b></u>
None.

***

<u><b>Constructor Parameters</b></u>
* 🟡 `_header` : `Header`
* 🟢 `_size` : `int`

***

<u><b>Instance Variables</b></u>
* 🟡 `header` : `Header`
* 🟢 `size` : `int`
* `buffers` : `array<buffer|brook_buffer_unset>`

***

<u><b>Static Methods</b></u>

<u>get_size</u>
* Description
	* Returns this Brook's `size` value.
* Return : `int`

<u>set_flag</u>
* Description
	* Inserts a buffer at the provided flag's corresponding index.
* Parameters
	* `flag` : `bitflag
	* `bufferIn` : `buffer

<u>build</u>
* Description
	* Constructs and returns a buffer containing containing the corresponding ordered Header data based on the currently set flags.
* Return : `buffer`

<u>buffer_compressed</u>
* Description
	* Creates a buffer with the `build` method, compresses, and returns it. The uncompressed version is deleted before the compressed copy is returned.
* Return : `buffer_compressed`
