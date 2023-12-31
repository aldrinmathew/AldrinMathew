![qat_colorful_cover](https://github.com/qatlang/media/raw/main/images/qat_fancy_cover.png)

Hi, this is Aldrin Mathew. I am the creator of the `qat` programming language. qat is envisioned to be a modern systems language for efficient and maintainable software...

<div><center>
<a href="https://github.com/qatlang/qat/releases"><img src="https://img.shields.io/badge/Download-444444?style=for-the-badge&logo=github&logoColor=white"/></a>
<a href="https://github.com/sponsors/aldrinmathew" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/SPONSOR-9900FF?style=for-the-badge&logo=github&logoColor=white"/></a>
<a href="https://qat.dev" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/qat.dev-444444?style=for-the-badge&logoColor=white"/></a>
<a href="https://youtube.com/c/aldrinmathew" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white"/></a>
<a href="https://discord.gg/CNW3Uvptvd" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/Discord-3366DD?style=for-the-badge&logo=discord&logoColor=white"/></a>
</div>

Here is some working code written in `qat`:

```rust
type StringBase:[T] {
	data :: multiptr:[var T, heap].
	len :: usize.

	pub default [
		''data := null.
		''len := 0.
	]

	pub from (val :: str) [
		''data := null.
		''len := 0.
		if (val'length != 0) [
			''data = heap:get:[T](val'length).
			loop (val'length) : new i [
				''data[i] = val[i].
			]
			''len = val'length.
		]
	]

	pub copy other [
		''data := null.
		''len := 0.
		if (other'data != null) [
			''data = heap:get:[T](other'len).
			loop (other'len) : new i [
				''data[i] = other'data[i].
			]
			''len = other'len.
		]
	]

	pub operator copy = other [
		if (''data != null) [
			heap:put(''data).
		]
		if (other'data != null) [
			''data = heap:get:[T](other'len).
			loop (other'len) : new i [
				''data[i] = other'data[i].
			]
			''len = other'len.
		] else [
			''data = null.
			''len = 0.
		]
	]

	pub move other [
		''data := other'data.
		''len := other'len.
		other'data = null.
		other'len = 0.
	]

	pub operator move = other [
		if (''data != null) [
			heap:put(''data).
		]
		''data = other'data.
		''len = other'len.
		if (other'data != null) [
			other'data = null.
			other'len = 0.
		]
	]

	pub var:append -> ''
	(other :: self) [
		if (other'len > 0) [
			if ((''data'length - ''len) >= other'len) [
				loop (other'len) : new i [
					''data[i + ''len] = other'data[i].
				]
			] else [
				new newCap = ''len + (2 * other'len).
				new newData = heap:get:[T](newCap).
				loop (''len) : new i [
					newData[i] = ''data[i].
				]
				loop (other'len) : new j [
					newData[''len + j] = other'data[j].
				]
				heap:put(''data).
				''data = newData.
				''len = ''len + other'len.
			]
		]
		give ''.
	]

	pub var:append_str -> ''
	(other:: str) [
		''var:append(self from (other)).
		give ''.
	]

	pub var:operator << -> ''
	(other :: str) [
		''var:append(self from (other)).
		give ''.
	]

	pub getCapacity -> usize
	() [
		give ''data'length.
	]

	pub var:extendCapacity(length :: usize) [
		if ((length > ''data'length) && (''data != null)) [
			new newPtr = heap:grow:[u8](''data, length).
			if (newPtr != null) [
				heap:put(''data).
				''data = newPtr.
			]
		] else if (''data == null) [
			''data = heap:get:[u8](length).
		]
	]

	pub length -> usize
	() [
		give ''len.
	]

	pub get_data -> multiptr:[T]
	() [
		give ''data to multiptr:[T].
	]

	pub var:get_data -> multiptr:[var T]
	() [
		give ''data to multiptr:[var T].
	]

	pub operator + -> self
	(other :: self) [
		new var res = ''copy.
		res'var:append(other'move).
		give res'move.
	]

	pub operator + -> self
	(other :: str) [
		new var res = ''copy.
		res'var:append_str(other).
		give res'move.
	]

	pub operator [] -> T
	(index :: usize) [
		give ''data[index].
	]

	pub end [
		if (''data != null) [
			heap:put(''data).
		]
	]
}

type String = StringBase:[u8].
```
