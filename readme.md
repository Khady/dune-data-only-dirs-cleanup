Dune does not fully cleanup _build for directories marked as data only.

```
$ dune clean
$ cat from_spec_a.sexp 
6
$ ls -l spec_a/**/*.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:16 spec_a/d1/1.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:16 spec_a/d1/2.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:16 spec_a/d1/3.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:32 spec_a/d2/1.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:32 spec_a/d2/2.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:32 spec_a/d2/3.txt
$ dune build @gen_spec_a
$ tree _build/default/spec_a
_build/default/spec_a
├── d1
│   ├── 1.txt
│   ├── 2.txt
│   └── 3.txt
└── d2
    ├── 1.txt
    ├── 2.txt
    └── 3.txt

2 directories, 6 files
$ rm -rf spec_a/d2
$ dune build @gen_spec_a
$ ls -l spec_a/**/*.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:16 spec_a/d1/1.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:16 spec_a/d1/2.txt
-rw-r--r-- 1 louis louis 0 Aug  2 10:16 spec_a/d1/3.txt
$ tree _build/default/spec_a
_build/default/spec_a
├── d1
│   ├── 1.txt
│   ├── 2.txt
│   └── 3.txt
└── d2
    ├── 1.txt
    ├── 2.txt
    └── 3.txt

2 directories, 6 files
$ cat from_spec_a.sexp 
6
```
