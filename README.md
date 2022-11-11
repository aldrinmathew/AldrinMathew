![qat_colorful_cover](https://github.com/qatlang/media/raw/main/images/qat_fancy_cover.png)

Hi, I am the creator of `qat` programming language. qat is envisioned to be a superfast, modern systems language for efficient and maintainable software...

<div><center>
<a href="https://github.com/qatlang/qat/releases"><img src="https://img.shields.io/badge/Download-444444?style=for-the-badge&logo=github&logoColor=white"/></a>
<a href="https://github.com/sponsors/aldrinmathew" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/SPONSOR-9900FF?style=for-the-badge&logo=github&logoColor=white"/></a>
<a href="https://qat.dev" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/qat.dev-444444?style=for-the-badge&logoColor=white"/></a>
<a href="https://youtube.com/c/aldrinmathew" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white"/></a>
<a href="https://discord.gg/CNW3Uvptvd" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/Discord-3366DD?style=for-the-badge&logo=discord&logoColor=white"/></a>
</div>

Here's how much time tracked of me working on the compiler for qat: [![Wakatime](https://wakatime.com/badge/user/af510812-c60b-4a16-bb6e-fada8313362b/project/e1c4e435-cfac-41ac-9ba3-59d61be2f357.svg)](https://qat.dev). Add about 400 hours to this, because time tracking was enabled a few months after the project started. The work on the compiler started in November 2021. The first commit was on 13th December 2021, but there were a few scrapped versions before that.

**I have spent a significant amount of time and effort on the language project, so if you appreciate that effort and you are able to support financially, consider sponsoring me on [Github Sponsors](https://github.com/sponsors/aldrinmathew). If you are not able to donate, but still want to show appreciation, drop into our [Discord Server](https://discord.gg/CNW3Uvptvd)**

Here's a preview of the syntax of `qat`:

```qat
main -> i32
() [
   say "Hello, World!".
   new
   give 0.
]

type String {
   buffer :: #[var u8].
   len    :: usize    .
   cap    :: usize    .

   pub:

   from (str val) [
      ''buffer = heap'get'<u8>(val'length).
      ''len = val'length.
      ''cap = val'length.
      loop (val'length) : new I [
         ''buffer[I] = val[I].
      ]
   ]

   display() [
      say'only str{''buffer, ''len}.
   ]

   end [
      heap'put(''buffer).
      ''len = 0.
      ''cap = 0.
   ]
}
```

![Profile views](https://gpvc.arturio.dev/AldrinMathew)
