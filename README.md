# Installation and Usage Documentation

In our experiment, Smartverif tool is run on a PC server with Ubuntu 16.04 LTS.

## Installing Dependencies

```
$ sudo apt-get install maude graphviz haskell-stack
$ stack upgrade
```

## Compiling Tamarin Prover

```
$ git clone https://github.com/tamarin-prover/tamarin-prover.git
$ cd tamarin-prover
$ make default
```

After the compilation, `tamarin-prover` executable will be copied to `~/.local/bin` directory.
Add the directory to your PATH.

`export PATH=$PATH:~/.local/bin`

To use SmartVerif, you need to confirm that `tamarin-prover` can be executed on current shell.

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

## Installing Python Environment

Install [Anaconda Python 3 version](https://www.anaconda.com/distribution/) and execute the following to install packages.

```
$ conda install tensorflow python-levenshtein numpy pandas
```


## Using SmartVerif

For example, execute the following command to use SmartVerif to verify the model `example.spthy`.

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
The messages starting from `summary of summaries` demonstrate the result of verification.