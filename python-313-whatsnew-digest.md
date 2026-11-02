# Python 3.13 What's New — Digest

Distilled from the official Python 3.13 release notes for a study-group handout.

## Highlights

- **Free-threaded CPython (PEP 703)**: experimental support for running with the GIL disabled; use `python3.13t` or `--disable-gil`; check with `sys._is_gil_enabled()`; optionally `PYTHON_GIL` or `-X gil=1` at runtime.
- **Experimental JIT compiler (PEP 744)**: built with `--enable-experimental-jit`; hot Tier 1 bytecode is translated to a Tier 2 IR and then to machine code (new build-time dependency on LLVM); disable at runtime with `PYTHON_JIT=0`.
- **Defined `locals()` semantics (PEP 667)**: optimized scopes (functions, generators, coroutines, comprehensions) now return independent snapshots; `FrameType.f_locals` returns a write-through proxy.
- **Type parameters support defaults (PEP 696)**: `typing.TypeVar`, `typing.ParamSpec` and `typing.TypeVarTuple` now accept default values.
- **`warnings.deprecated()` decorator (PEP 702)**: communicate deprecations to static type checkers and warn at runtime.
- **`typing.ReadOnly` (PEP 705)**: mark a `typing.TypedDict` item as read-only for type checkers.
- **`typing.TypeIs` (PEP 742)**: more intuitive type narrowing as an alternative to `typing.TypeGuard`.
- **Mobile and WASI platform support**: iOS and Android now tier 3 supported (PEP 730, PEP 738); `wasm32-wasi` is tier 2; `wasm32-emscripten` is no longer supported.
- **Security**: `ssl.create_default_context()` now sets `ssl.VERIFY_X509_PARTIAL_CHAIN` and `ssl.VERIFY_X509_STRICT` as default flags.
- **Removed "dead batteries" (PEP 594)**: 19 legacy modules removed (`aifc`, `audioop`, `cgi`, `cgitb`, `chunk`, `crypt`, `imghdr`, `mailcap`, `msilib`, `nis`, `nntplib`, `ossaudiodev`, `pipes`, `sndhdr`, `spwd`, `sunau`, `telnetlib`, `uu`, `xdrlib`); also removed `2to3`/`lib2to3`, `tkinter.tix`, `locale.resetlocale()`, `typing.io`/`typing.re`, and chained `classmethod` descriptors.
- **New interactive interpreter**: multiline editing with history, color prompts and tracebacks, F1 help, F2 history browsing, F3 paste mode; disable with `PYTHON_BASIC_REPL`.
- **Improved error messages**: colored tracebacks by default (`PYTHON_COLORS`, `NO_COLOR`, `FORCE_COLOR`), helpful messages when a script shadows a stdlib/third-party module, and suggestions for misspelled keyword arguments.
- **New functions and modules**: `dbm.sqlite3` (default `dbm` backend), `base64.z85encode()`/`z85decode()`, `math.fma()`, `statistics.kde()`/`kde_random()`, `pathlib.Path.from_uri()`, `PurePath.full_match()`, `Path.glob()`/`rglob()` `recurse_symlinks`, `random` command-line interface, `os.process_cpu_count()`, `mmap.seekable()`, `traceback ExcType_str`, `typing.get_protocol_members()`/`is_protocol()`, `types.SimpleNamespace` single positional argument.
- **Porting policy (PEP 602)**: 3.13 and later get two years of full (bugfix) support followed by three years of security fixes.

## Notable deprecations

- `array` `'u'` format code deprecated at runtime (remove in 3.16); use `'w'` for Unicode characters.
- `ctypes.SetPointerType()` deprecated (remove 3.15); `ARRAY()` soft-deprecated in favour of `type * length` multiplication.
- `decimal` format specifier `'N'` deprecated (remove 3.18); only supported in the C implementation.
- `dis.HAVE_ARGUMENT` separator deprecated; use `hasarg` instead.
- `gettext` non-integer plural-form arguments deprecated.
- `glob.glob0()` and `glob1()` deprecated; use `glob()` with the `root_dir` parameter.
- `http.server.CGIHTTPRequestHandler` and the `--cgi` flag deprecated (remove 3.15).
- `mimetypes.guess_type()` path arguments soft-deprecated; use `guess_file_type()`.
- `re.split()`, `re.sub()` and `re.subn()` positional `maxsplit`, `count` or `flags` arguments deprecated; these become keyword-only.
- `pathlib.PurePath.is_reserved()` deprecated (remove 3.15); use `os.path.isreserved()`.
- `platform.java_ver()` deprecated (remove 3.15); only useful for Jython.
- `pydoc.ispackage()` deprecated.
- `sqlite3`: passing more than one positional argument to `connect()`/constructor deprecated (keyword-only in 3.15); passing the callable, name and number of arguments as keywords to `Connection.create_function()`/`create_aggregate()` deprecated (positional-only in 3.15).
- `sys._enablelegacywindowsfsencoding()` deprecated (remove 3.16); use `PYTHONLEGACYWINDOWSFSENCODING`.
- `tarfile.TarFile.tarfile` attribute deprecated (remove 3.16).
- `traceback.TracebackException.exc_type` deprecated; use `exc_type_str`.
- `typing`: functional `NamedTuple` keyword arguments, omitting or passing `None` for `fields` on `NamedTuple`/`TypedDict`, `@typing.no_type_check_decorator`, and `typing.AnyStr` (remove from `__all__` in 3.16, `DeprecationWarning` on import, removed entirely in 3.18).
- `wave.getmark()`/`setmark()`/`getmarkers()` deprecated (remove 3.15).

Pending removal in 3.14: `ast.Num`/`Str`/`Bytes`/`NameConstant`/`Ellipsis` (emit `DeprecationWarning`, remove 3.14); `asyncio` child-watcher classes and `get_event_loop()` warning; `importlib.abc.ResourceReader`/`Traversable`/`TraversableResources`; `itertools` pickle/deepcopy/copy burden; `multiprocessing` default start-method change on Linux/BSD; `pathlib.is_relative_to`/`relative_to` additional arguments; `pkgutil.find_loader()`/`get_loader()`; `pty.master_open()`/`slave_open()`; `sqlite3.version`/`version_info` and `execute()`/`executemany()` with named placeholders as a sequence; `urllib.parse.Quoter`.

Pending removal in 3.15: setting `__cached__` without `__spec__.cached`; `ctypes.SetPointerType()`; `http.server.CGIHTTPRequestHandler`/`--cgi`; `importlib` `load_module()`; `pathlib.PurePath.is_reserved()`; `platform.java_ver()`; `sysconfig.is_python_build(check_home)`; `threading.RLock()` arguments; `types.CodeType.co_lnotab` (PEP 626).

## Source

Source: "What's New In Python 3.13" — https://docs.python.org/3/whatsnew/3.13.html (read today; Python 3.13 released October 7, 2024).
