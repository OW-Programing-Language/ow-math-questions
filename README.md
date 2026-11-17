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
