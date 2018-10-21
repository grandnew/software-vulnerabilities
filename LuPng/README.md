# Heap Buffer Overflow in Function internalPrintf

I used **clang 6.0 and AddressSanitizer**  to build **[LuPng](https://github.com/jansol/LuPng)**, this [file](https://github.com/grandnew/software-vulnerabilities/blob/master/LuPng/heap-buffer-overflow_internalPrintf) can cause heap buffer overflow in function internalPrintf in lupng.c when executing this command:

```shell
./lupng heap-buffer-overflow_internalPrintf 1.png
```

This is the ASAN information:

```shell
=================================================================
==19423==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x602000000073 at pc 0x0000004478f1 bp 0x7ffea55195f0 sp 0x7ffea5518da0
READ of size 4 at 0x602000000073 thread T0
    #0 0x4478f0 in printf_common(void*, char const*, __va_list_tag*) /home/fouzhe/llvm/llvm/projects/compiler-rt/lib/asan/../sanitizer_common/sanitizer_common_interceptors_format.inc:548
    #1 0x44836a in __interceptor_vfprintf /home/fouzhe/llvm/llvm/projects/compiler-rt/lib/asan/../sanitizer_common/sanitizer_common_interceptors.inc:1549
    #2 0x52d470 in internalPrintf /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:286:5
    #3 0x51d69f in readChunk /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:758:9
    #4 0x51d69f in luPngReadUC /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:812
    #5 0x520b90 in luPngReadFile /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:859:15
    #6 0x515cff in main /home/fouzhe/my_fuzz/LuPng/miniz/example.c:23:11
    #7 0x7f9278c7382f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #8 0x41a028 in _start (/home/fouzhe/my_fuzz/LuPng/miniz/lupng+0x41a028)

0x602000000073 is located 0 bytes to the right of 3-byte region [0x602000000070,0x602000000073)
allocated by thread T0 here:
    #0 0x4de258 in __interceptor_malloc /home/fouzhe/llvm/llvm/projects/compiler-rt/lib/asan/asan_malloc_linux.cc:88
    #1 0x516c35 in readChunk /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:742:30
    #2 0x516c35 in luPngReadUC /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:812
    #3 0x520b90 in luPngReadFile /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:859:15
    #4 0x515cff in main /home/fouzhe/my_fuzz/LuPng/miniz/example.c:23:11

SUMMARY: AddressSanitizer: heap-buffer-overflow /home/fouzhe/llvm/llvm/projects/compiler-rt/lib/asan/../sanitizer_common/sanitizer_common_interceptors_format.inc:548 in printf_common(void*, char const*, __va_list_tag*)
Shadow bytes around the buggy address:
  0x0c047fff7fb0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c047fff7fc0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c047fff7fd0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c047fff7fe0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c047fff7ff0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0c047fff8000: fa fa 00 fa fa fa 00 fa fa fa fd fa fa fa[03]fa
  0x0c047fff8010: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff8020: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff8030: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff8040: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff8050: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
==19423==ABORTING
```



# Heap Buffer Overflow in Function insertByte(577:55)

I used **clang 6.0 and AddressSanitizer**  to build **[LuPng](https://github.com/jansol/LuPng)**, this [file](https://github.com/grandnew/software-vulnerabilities/blob/master/LuPng/heap-buffer-overflow_insertByte_577) can cause heap buffer overflow in function insertByte(577:55) in lupng.c when executing this command:

```shell
./lupng heap-buffer-overflow_insertByte_577 1.png
```

This is the ASAN information:

```shell
=================================================================
==20646==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x61d000000880 at pc 0x00000052ef4d bp 0x7ffde8e44f60 sp 0x7ffde8e44f58
WRITE of size 2 at 0x61d000000880 thread T0
    #0 0x52ef4c in insertByte /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:577:55
    #1 0x519ad1 in parseIdat /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:722:21
    #2 0x519ad1 in handleChunk /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:776
    #3 0x519ad1 in luPngReadUC /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:814
    #4 0x520b90 in luPngReadFile /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:859:15
    #5 0x515cff in main /home/fouzhe/my_fuzz/LuPng/miniz/example.c:23:11
    #6 0x7fa295ea382f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #7 0x41a028 in _start (/home/fouzhe/my_fuzz/LuPng/miniz/lupng+0x41a028)

0x61d000000880 is located 0 bytes to the right of 2048-byte region [0x61d000000080,0x61d000000880)
allocated by thread T0 here:
    #0 0x4de258 in __interceptor_malloc /home/fouzhe/llvm/llvm/projects/compiler-rt/lib/asan/asan_malloc_linux.cc:88
    #1 0x52c455 in luImageCreate /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:1213:32
    #2 0x51b7a2 in parseIhdr /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:477:17
    #3 0x51b7a2 in handleChunk /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:772
    #4 0x51b7a2 in luPngReadUC /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:814
    #5 0x520b90 in luPngReadFile /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:859:15
    #6 0x515cff in main /home/fouzhe/my_fuzz/LuPng/miniz/example.c:23:11

SUMMARY: AddressSanitizer: heap-buffer-overflow /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:577:55 in insertByte
Shadow bytes around the buggy address:
  0x0c3a7fff80c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c3a7fff80d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c3a7fff80e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c3a7fff80f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c3a7fff8100: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0c3a7fff8110:[fa]fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c3a7fff8120: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c3a7fff8130: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c3a7fff8140: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c3a7fff8150: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c3a7fff8160: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
==20646==ABORTING
```





# Heap Buffer Overflow in Function insertByte(598:37)

I used **clang 6.0 and AddressSanitizer**  to build **[LuPng](https://github.com/jansol/LuPng)**, this [file](https://github.com/grandnew/software-vulnerabilities/blob/master/LuPng/heap-buffer-overflow_insertByte_598) can cause heap buffer overflow in function insertByte(598:37) in lupng.c when executing this command:

```shell
./lupng heap-buffer-overflow_insertByte_598 1.png
```

This is the ASAN information:

```shell
=================================================================
==21120==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x6160000005de at pc 0x00000052eac5 bp 0x7ffe0a8090e0 sp 0x7ffe0a8090d8
WRITE of size 1 at 0x6160000005de thread T0
    #0 0x52eac4 in insertByte /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:598:37
    #1 0x519d0c in luPngReadUC /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:718:28
    #2 0x520b90 in luPngReadFile /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:859:15
    #3 0x515cff in main /home/fouzhe/my_fuzz/LuPng/miniz/example.c:23:11
    #4 0x7f54160b282f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #5 0x41a028 in _start (/home/fouzhe/my_fuzz/LuPng/miniz/lupng+0x41a028)

0x6160000005de is located 30 bytes to the right of 576-byte region [0x616000000380,0x6160000005c0)
allocated by thread T0 here:
    #0 0x4de258 in __interceptor_malloc /home/fouzhe/llvm/llvm/projects/compiler-rt/lib/asan/asan_malloc_linux.cc:88
    #1 0x52c455 in luImageCreate /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:1213:32
    #2 0x51b7a2 in parseIhdr /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:477:17
    #3 0x51b7a2 in handleChunk /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:772
    #4 0x51b7a2 in luPngReadUC /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:814
    #5 0x520b90 in luPngReadFile /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:859:15
    #6 0x515cff in main /home/fouzhe/my_fuzz/LuPng/miniz/example.c:23:11

SUMMARY: AddressSanitizer: heap-buffer-overflow /home/fouzhe/my_fuzz/LuPng/miniz/lupng.c:598:37 in insertByte
Shadow bytes around the buggy address:
  0x0c2c7fff8060: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c2c7fff8070: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c2c7fff8080: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c2c7fff8090: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c2c7fff80a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0c2c7fff80b0: 00 00 00 00 00 00 00 00 fa fa fa[fa]fa fa fa fa
  0x0c2c7fff80c0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c2c7fff80d0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c2c7fff80e0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c2c7fff80f0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c2c7fff8100: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
==21120==ABORTING
```

