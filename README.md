# BeforeHack
## Initial Thoughts/stuffs to explore
- What is AST? How does it work?
- How to use Typescript Compiler API effectively?
- How does UML Work?
- How do we visualize these?
- Detailed Stack/Methodology to choose
- Misc.
## AST
Just a simplified, condensed version of a [parse tree](https://t1.daumcdn.net/cfile/tistory/2468CD39516B9E2B30)!
![parse tree](https://t1.daumcdn.net/cfile/tistory/2468CD39516B9E2B30).
(parse tree takes account every detail of our code, from punctuation to expressions to tokens)

**Concrete Syntax Tree(CST) is more of a parse tree than AST**

### Parse Trees vs Syntax Trees
- Parse tree demonstrates what an expression looks like, which is the concrete syntax of a text
- Syntax tree shows important bits, only abstracted syntax

### Lexical Analysis, then Syntax Analysis in compiler
![lexical analysis](https://cdn-images-1.medium.com/max/900/1*2WYz6w470aMymWzmQKYLHQ.jpeg)
```text
source text => scanner => lexemes => lexer/tokenizer => tokens => parser
```
Parser takes tokens and makes a parser tree out of them like this:
![parser tree!](https://cdn-images-1.medium.com/max/1200/1*hy0NjQ4pe44ysbU_eKFaXg.jpeg)
**Parser tree represents the program by its most distinct parts, but it can be too extraaaaa**

### Where does AST come in?

From the previous pic, there are superfluous information, like expression parent node of 5, 1, 12 and parentheses, which have no significance
If we simplify the tree and rid of syntactic "dust", only these are left:
![AST!](https://cdn-images-1.medium.com/max/1200/1*T0Zo8ZLDDm0m0fSmmkj7wA.jpeg)

Heres takeaways:
1. Syntactic details are ignored, i.e., semi-colons, commas, and parentheses
2. Chains of nodes are collapsed; no single-successor nodes will remain
3. Operators will become parent nodes

Therefore, the final result of the syntax analysis phase is AST! The parser will always generate an AST as its output!

### Anatomy of an AST node

![anatomy of AST node](https://cdn-images-1.medium.com/max/1200/1*NO_p9739sX6Tf-ESRkSKaw.jpeg)
Every node in an AST has references to next sibling node or its first child node

```typescript
interface ASTNode {
  siblingNode ASTNode
  childNode ASTNode
}
```
So the previous expression can be abridged to this tree:
![AST result](https://cdn-images-1.medium.com/max/1200/1*0n73V3Ld0e-nTmZKGw3OpQ.jpeg)

These whole process, converting the code to CST+AST or just AST, or in other words lexical and syntax analysis, is so called as the analysis phase, or front-end of the compiler
Technically speaking, it's the **intermediate representation(IR)** of a program, which makes a data structure that is used by the compiler to represent a source text

## Typescript Compiler API
- [https://typescript-api-playground.glitch.me/#example=TypeScript%20scanner](https://typescript-api-playground.glitch.me/#example=TypeScript%20scanner)

## UML

## Project Structure
```text
AST -> json -> mapper -> PlantUML Builder -> template -> UML
```

### What do I need for UML out of ts AST
- Class Name: First Block of Class Diagram
- Access `modifiers` + `PropertyDeclaration`: Second Block of Class UML
- `modifiers` + `MethodDeclaration` + `Parameter` + `returnType` Third Block of Class UML
- `typeChecker` for method return, parameters, variables, etc
- probabily signature

### Mapping UML Builder by relationship
- Generalization
- Dependency
- Realization
- Composition
- Aggregation
- Reflexive
- Association / Direct Association
### Mapping Hierarchy
TODO: How to implement mapping hierarchy
## Graphing Methodology
### Possible candidates
- [node-graphviz](https://github.com/glejeune/node-graphviz)
  - [https://github.com/joaompneves/tsviz/blob/1e21243b92fe3ee0749dd540d7032ee6f4137852/src/uml-builder.ts#L8](https://github.com/joaompneves/tsviz/blob/1e21243b92fe3ee0749dd540d7032ee6f4137852/src/uml-builder.ts#L8)
- online sequence diagram tools
  - [sequencediagram.org]()
  - [yuml.me](https://yuml.me/)

## Useful Resource
- [https://yuml.me/](https://yuml.me/)
- [https://blog.scottlogic.com/2017/05/02/typescript-compiler-api-revisited.html](https://blog.scottlogic.com/2017/05/02/typescript-compiler-api-revisited.html)

## Revelant Code Analysis
- [https://github.com/fsahmad/typescript-uml/blob/c17b32ca510a256d9819a6028be3a77f93d9481a/src/delint.ts#L1](https://github.com/fsahmad/typescript-uml/blob/c17b32ca510a256d9819a6028be3a77f93d9481a/src/delint.ts#L1)
- Please checkout this... [https://github.com/Microsoft/TypeScript/wiki/Using-the-Compiler-API](https://github.com/Microsoft/TypeScript/wiki/Using-the-Compiler-API)
- [https://astexplorer.net/](https://astexplorer.net/)
- [https://typescript-api-playground.glitch.me/#example=TypeScript%20scanner](https://typescript-api-playground.glitch.me/#example=TypeScript%20scanner)
- [https://basarat.gitbooks.io/typescript/content/docs/compiler/ast.html](https://basarat.gitbooks.io/typescript/content/docs/compiler/ast.html)
- [https://gmlwjd9405.github.io/2018/07/04/class-diagram.html](https://gmlwjd9405.github.io/2018/07/04/class-diagram.html)
- [http://www.nextree.co.kr/p6753/](http://www.nextree.co.kr/p6753/)

## Reference

- [https://medium.com/basecs/grammatically-rooting-oneself-with-parse-trees-ec9daeda7dad](https://medium.com/basecs/grammatically-rooting-oneself-with-parse-trees-ec9daeda7dad)
- [https://medium.com/basecs/leveling-up-ones-parsing-game-with-asts-d7a6fc2400ff](https://medium.com/basecs/leveling-up-ones-parsing-game-with-asts-d7a6fc2400ff)
