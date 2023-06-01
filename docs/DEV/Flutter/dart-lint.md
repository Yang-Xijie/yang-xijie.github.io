# 设置 Dart 的 linter 规则

> Flutter 3.10.2, Dart 3.0.2

新建项目之后，在 `analysis_options.yaml` 的 `linter > rules` 下面添加 `prefer_const_*` 以防止 `Dart` 不停提示添加或移除 `const`（非实际项目）：

```yml
include: package:flutter_lints/flutter.yaml
linter:
  # A list of all available lints and their documentation is published at
  # https://dart-lang.github.io/linter/lints/index.html.
  rules:
    prefer_const_constructors: false
    prefer_const_constructors_in_immutables: false
    prefer_const_literals_to_create_immutables: false
    # avoid_print: false  # Uncomment to disable the `avoid_print` rule
    # prefer_single_quotes: true  # Uncomment to enable the `prefer_single_quotes` rule
```

## References

https://medium.com/podiihq/setting-up-lint-rules-in-dart-flutter-1ebbed0418a6
