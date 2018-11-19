# BeforeHack
## Initial Thoughts/stuffs to explore
- What is AST? How does it work?
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

## Useful Resource
- [https://yuml.me/](https://yuml.me/)

## Reference

- [https://medium.com/basecs/grammatically-rooting-oneself-with-parse-trees-ec9daeda7dad](https://medium.com/basecs/grammatically-rooting-oneself-with-parse-trees-ec9daeda7dad)
- [https://medium.com/basecs/leveling-up-ones-parsing-game-with-asts-d7a6fc2400ff](https://medium.com/basecs/leveling-up-ones-parsing-game-with-asts-d7a6fc2400ff)
