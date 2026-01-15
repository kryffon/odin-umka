# odin-umka

[Odin](https://odin-lang.org/) bindings for [umka](https://github.com/vtereshkov/umka-lang) 1.5.5

- umprof ported from https://github.com/marekmaskarinec/umprof

## Usage

```odin
umka_code: cstring = /* some umka code */

U := umka.Alloc()
ok := umka.Init(U, "main.um", umka_code, 1024 * 1024, nil, argc, raw_data(argv), false, false, umka.PrintCompileWarning)

when UMPROF {
		if ok do umka.umprofInit(U)
}

// add umka modules here
if ok do ok = umka.Compile(U)

if ok {
		exitcode := umka.Run(U)
		if exitcode != 0 do umka.PrintRuntimeError(U)
} else {
		umka.PrintCompileError(U)
}

when UMPROF {
		umka.umprofPrintTable()
		umka.umprofDinit()
}

umka.Free(U)
```
