env = Environment(CC = 'cl',
                   CCFLAGS = ['/EHsc','/O2','/TC','/std:c17'])

cpppath = ['./']
cppdefines = ['CONFIG_BIGNUM']#{'CONFIG_VERSION': '\"2024-02-14\"'}
src = ["./quickjs.c", "./libregexp.c",  "./libunicode.c",  "./cutils.c",  "./quickjs-libc.c",  "./libbf.c"]

qjsc_prog = env.Program("out/qjsc", ["./qjsc.c"]+src, CPPPATH=cpppath, CPPDEFINES=cppdefines)

current_path = Dir('.').srcnode().abspath

cmd_repl = env.Command("./repl.c", "./repl.js", current_path + "\\out\\qjsc.exe -c -o $TARGET -m $SOURCE")
Depends(cmd_repl, qjsc_prog)

cmd_qjscalc = env.Command("./qjscalc.c", "./qjscalc.js", current_path + "\\out\\qjsc.exe -c -o $TARGET $SOURCE")
Depends(cmd_qjscalc, qjsc_prog)

qjs_prog = env.Program("out/qjs", ["./qjs.c","./repl.c","./qjscalc.c"]+src, CPPPATH=cpppath, CPPDEFINES=cppdefines)
Depends(qjs_prog, cmd_repl + cmd_qjscalc)
