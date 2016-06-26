https://www.youtube.com/watch?v=iKyIKozv8a8
Principles for Modular, Functional, Approachable Libraries — Erik
Osheim
# Functional
  1. Use type classes for open interfaces.
  2. Encourage/require laws for type classes/data types.
  3. Encourage/require referential transparency (i.e. purity)
  4. First-class laziness support.
  5. Encourage composition.
  6. Support abstraction, minimize duplication.
  7. Watch other libraries, languages, and researchers.

# Safe
  1. Stack-safe by default
  2. Express partiality with values not exceptions
  3. Minimize allocations where possible
  4. Property-based testing
  5. Aim for 100% test coverage
  6. Benchmarking and "real world" tests

# Fast
  1. Avoid inefficient default implementations.
  2. Do benchmarking and profiling.
  3. Perform manual/mechanical optimizations if possible
  4. Design "low-level" abstractions with perfomance in mind.
  5. Make common syntax/usage efficient.

# Documentation
  1. Require Type-checked tutorials and documentation
  2. Require ScalaDoc on methods/classes
  3. Create docs for users, contributers, maintainers
  4. Err on the side of more prose rather than less.
  5. Link to the literature where possible.
  6. Major design discussions should occure on Github/Gitter.

# Modular
  1. Platform independent by default(cats.jvm/cats.js)
  2. Non-monolithic, limited scope
  3. Extensible, extensibility hooks
  4. Publish laws and test-hooks for third-parties
  5. Move small, useful utilities to standalone projects
  6. Use / support other libraries

# Idiomatic
  1. Explicitly mark/differentiate type classes
  2. Minimize boilerplate where possible
  3. Support built-in Scala types by default
  4. Discuss and enforce common coding conventions
  5. Consider and standardize on language extensions

# Pragmatic
  1. Projects may "dial-in" their strictness (e.g.alleycats)
  2. Allow specific, thoughtful exceptions (e.g. Double)
  3. Agressively listen to and respond to "pain points"
  4. Willing to specialize the critical path
  5. All features should have concrete motivating examples

# Collabrative
  1. Give many people authority
  2. Provide quick feedback on issues and PRs
  3. Requer 2 sing-ofss on PR merging
  4. Encourage discussion on issues/PRs
  5. Leave opportunities for newcomers when possible.

# Welcoming
  1. Be clear on expectations around conduct
  2. Try to model productive and helpful behavior
  3. Work to aim documentation towards newcomers
  4. Reach out to the wider programming community.


#Type classes
`def log[A : Show](a: A) = println(implicitly[Show[A]].show(a))` is
 the same as:
`def log[A](a: A)(implicit s: Show[A]) = println(s.show(a))`. For
`trait Show[A] { def show(f: A): String}`

