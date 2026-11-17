# ow-math-questions

A reusable **100% OW** arithmetic question-generation library for OW games and learning apps.

Provides an `MathQuestions` class for configurable arithmetic questions, exact-division generation, answer checking, and multiple-choice distractors. It intentionally leaves difficulty settings, scoring, progression, and interface logic to the consuming application.

## Usage

```ow
import "src/MathQuestions.ow"

main:
  set generator: new MathQuestions()
  set question: generator.generate_any(["+", "-", "*", "/"], 1, 10)
  print: question.prompt
  print: generator.choices(question, 4)
```

Supported operations: `+`, `-`, `*`, `/`, `%`, `^` and `pow` (alias). Builtins such as `rand`, `mod` and `pow` belong to the OW runtime, not this library.

## Use as an OW project dependency

With an OW compiler that supports `dependencies.yml`, you can add this
library once to your project's root manifest:

```yaml
format: 1
repositories:
  - id: github
    url: https://github.com
dependencies:
  - name: math
    repository: github
    path: OW-Programing-Language/ow-math-questions
    version: c22d01cfee6be18d96d4c55b95b7e79892bca9f6
```

In an OW source file, import the library by its declared alias:

```ow
import "@math/src/MathQuestions.ow"

main:
  set generator: new MathQuestions()
  set q: generator.generate_any(["+", "-", "*", "/"], 1, 10)
  print: q.prompt
```

Run `ow deps install` (or simply `ow run main.ow` for auto-resolution).
The lockfile `dependencies.lock.yml` pins the exact Git commit. See
[OW's dependency documentation](https://github.com/OW-Programing-Language/ow-lang/blob/main/docs/dependencies.md)
for all commands and options.

## Run

```sh
ow run examples/quiz_demo.ow
ow run examples/math_skill_adapter.ow
ow check tests/math_questions_test.ow
ow run tests/math_questions_test.ow
```

## API

- `random_int(low, high)` — inclusive random integer
- `calculate(op, a, b)` — arithmetic operation
- `from_operands(op, a, b)` — explicit question
- `generate(op, low, high)` — beginner-safe random question
- `generate_any(operations, low, high)` — random operation from allowed set
- `choices(question, count)` — 2–6 distinct possible answers
- `is_correct(question, proposed_answer)` — correctness check

`generate()` uses nonnegative subtraction results, nonzero divisors, exact integer division, and capped exponents. This is a prototype and should be checked with the currently installed OW interpreter before production use.

## License

MIT — see [LICENSE](LICENSE).
