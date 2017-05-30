# clang-callgraph
A tool which generate a call graph from a given C++ based on clang. It excludes
calls to the standard library so that only what matters to your app is shown.

# Usage

`./clang-callgraph.py file.cpp|compile_commands.json [extra clang args...]`

The easiest way to generate the file compile\_commands.json for any make based
compilation chain is to use Bear and recompile with `bear make`.

When running the python script, after parsing all the codebase, you are
prompted to type in the function's name for which you wan to obtain the
callgraph

# Example

```
$ bear make
<output omitted>
$ python2 ~/oauth_krb5/clang-analyze.py compile_commands.json -I/usr/lib/llvm-3.8/lib/clang/3.8.0/include/
reading source files...
/home/vermeille/CPAsim/src/module.cpp
/home/vermeille/CPAsim/src/module/modulevalues.cpp
/home/vermeille/CPAsim/src/main.cpp
/home/vermeille/CPAsim/src/parser.cpp
> main
matching:
main(int, char **)
> main(int, char **)
main(int, char **)
  Parser::ParseModuleDef(std::istream &)
    Parser::EatWord(std::istream &, const std::string &)
      Parser::FuckSpaces(std::istream &)
      Parser::EatChar(std::istream &, char)
    Parser::ParseWord(std::istream &)
      Parser::FuckSpaces(std::istream &)
    Module::Module(const std::string &)
    Parser::FuckSpaces(std::istream &)
    Parser::EatChar(std::istream &, char)
    Parser::FuckSpaces(std::istream &)
    Parser::EatChar(std::istream &, char)
    Module::AddInput(std::unique_ptr<WireDecl>)
      WireDecl::name()
      WireDecl::name()
      WireDecl::name()
    Parser::ParseWireDecl(std::istream &)
      Parser::ParseWord(std::istream &)
      Parser::FuckSpaces(std::istream &)
      Parser::EatChar(std::istream &, char)
      Parser::FuckSpaces(std::istream &)
      Parser::ParseDecimalInt(std::istream &)
        Parser::FuckSpaces(std::istream &)
      Parser::FuckSpaces(std::istream &)
      Parser::EatChar(std::istream &, char)
      Parser::FuckSpaces(std::istream &)
      WireDecl::WireDecl(const std::string &, int)
```

