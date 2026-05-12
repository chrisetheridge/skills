# Smells and Techniques

Use code smells as prompts to investigate. A smell is not proof that code is wrong.

## Smell Prompts

- **Long method** - Use named steps when they expose intent. Avoid extraction that scatters local context.
- **Large class/module** - Split distinct concepts. Keep cohesive modules together.
- **Duplicate code** - Separate shared concepts from similar shape.
- **Primitive obsession** - Introduce a named value/object when it concentrates validation and meaning.
- **Long parameter list** - Look for a concept or options object.
- **Divergent change** - Split modules that change for unrelated reasons.
- **Shotgun surgery** - Concentrate concepts that require edits across many files.
- **Feature envy** - Move behavior closer to the data or concept it uses most.
- **Message chains** - Hide internal navigation from callers.
- **Dead code** - Delete it after you verify no caller depends on it.
- **Speculative generality** - Keep abstractions that serve real variation.

## Technique Menu

- **Rename** when the current name hides intent or domain language.
- **Extract variable/function** when a named concept makes the caller easier to read.
- **Inline variable/function** when a name adds indirection without meaning.
- **Decompose conditional** when branches mix policy, mechanics, and edge cases.
- **Introduce parameter object** when a set of parameters travels together and has shared meaning.
- **Move function/field** when behavior belongs with another module.
- **Extract class/module** when a larger module hides a cohesive concept.
- **Inline class/module** when a wrapper adds no leverage.
- **Replace conditional with polymorphism/strategy** when real variation exists.
- **Replace magic value with named constant/type** when the value carries domain meaning.
- **Delete** when a branch, wrapper, adapter, flag, or test no longer protects behavior.

## Abstraction Guardrails

Before extracting shared code, check:

- Name the concept in the domain.
- Show how the abstraction reduces caller knowledge.
- Show how future changes concentrate in one place.
- Apply the deletion test: deleting the abstraction should move complexity back to callers.
- Require at least two real uses, or one use plus a clear near-term change.

If those answers are weak, leave duplication in place or make a smaller local refactor.

## Source Influences

- Martin Fowler and Kent Beck: small behavior-preserving transformations; code smells as investigation prompts.
- Refactoring.Guru: stepwise refactoring, tests after each change, smell and technique taxonomy.
- Robert C. Martin: meaningful names, focused functions, readable code, tests.
- John Ousterhout: deep modules and simple interfaces.
- Sandi Metz: duplication can be cheaper than the wrong abstraction.
