# 安装使用指南

## 测试环境

Ubuntu LTS 16.04

## 安装依赖

```
$ sudo apt-get install maude graphviz haskell-stack
$ stack upgrade
```

## 编译安装tamarin prover

```
$ git clone https://github.com/tamarin-prover/tamarin-prover.git
$ cd tamarin-prover
$ make default
```

编译完成后tamarin-prover可执行程序会被复制到`~/.local/bin`目录下，然后将该目录加入到系统PATH中

`export PATH=$PATH:~/.local/bin`

然后确认当前shell可执行`tamarin-prover`程序

```
$ tamarin-prover 
error: no input files given

tamarin-prover [COMMAND] ... [OPTIONS] FILES
  Security protocol analysis and verification.

Commands:
  interactive  Start a web-server to construct proofs interactively.
  variants     Compute the variants of the intruder rules for DH-exponentiation.
  test         Self-test the tamarin-prover installation.

Flags:
     --prove[=LEMMAPREFIX]                   Attempt to prove a lemma
     --stop-on-trace[=DFS|BFS|NONE]          How to search for traces (default DFS)
  -b --bound[=INT]                           Bound the depth of the proofs
     --heuristic[=(s|S|o|O|p|P|l|c|C|i|I)+]  Sequence of goal rankings to use (default 's')
     --partial-evaluation[=SUMMARY|VERBOSE]  Partially evaluate multiset rewriting system
  -D --defines[=STRING]                      Define flags for pseudo-preprocessor.
     --diff                                  Turn on observational equivalence mode using diff terms.
     --quit-on-warning                       Strict mode that quits on any warning that is emitted.
     --oraclename[=FILE]                     Path to the oracle heuristic (default './oracle').
     --no-compress                           Do not use compressed sequent visualization
     --parse-only                            Just parse the input file and pretty print it as-is
  -o --output[=FILE]                         Output file
  -O --Output[=DIR]                          Output directory
     --with-dot[=FILE]                       Path to GraphViz 'dot' tool
     --with-json[=FILE]                      Path to JSON rendering tool (not working with --diff)
     --with-maude[=FILE]                     Path to 'maude' rewriting tool
About:
  -? --help                                  Display help message
  -V --version                               Print version information

------------------------------------------------------------------------------
See 'https://github.com/tamarin-prover/tamarin-prover/blob/master/README.md'
for usage instructions and pointers to examples.
------------------------------------------------------------------------------
```

## 安装Python3及相关库

安装[Anaconda Python 3 version](https://www.anaconda.com/distribution/)
然后运行以下命令安装相关库

```
$ conda install tensorflow python-levenshtein numpy pandas
```


## 使用SmartVerif

例如，使用SmartVerif验证协议模型文件`example.spthy`

```
$ ./smartverif example.spthy
Verification Starts
maude tool: 'maude'
 checking version: 2.7. OK.
 checking installation: OK.
SAPIC tool: 'sapic'
Checking availablity ... OK.

  solved goal nr. 0 (directly): SessKeyC( S, k.1 ) @ #i.2
  solved goal nr. 1 (directly): K( k.1 ) @ #j.3
  solved goal nr. 0 (directly): !Ltk( t.1, t.2 ) ▶₀ #i
  solved goal nr. 0 (directly): !Pk( t.1, t.2 ) ▶₀ #i
  solved goal nr. 0 (directly): Client_1( t.1, t.2 ) ▶₀

...

==============================================================================
summary of summaries:

analyzed: /home/sucheng/tamarin1/examples/Tutorial.spthy

  Client_session_key_secrecy (all-traces): verified
  Client_auth (all-traces): verified
  Client_auth_injective (all-traces): verified
  Client_session_key_honest_setup (exists-trace): verified

==============================================================================
```
上面的summary of summaries即为验证结果