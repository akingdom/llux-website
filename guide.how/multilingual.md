# Multilingual Llux

Llux is designed so source code can be written with localised keywords. Keyword maps translate human-language terms into the canonical language model before parsing.

## How It Works

1. A keyword map defines the terms for a language.
2. The compiler translates those terms into canonical Llux constructs.
3. The rest of the build pipeline works the same way as English source.

Keyword maps and locale files are planned as part of the public toolchain.

## Example Direction

The first public examples should include at least one English source file and one translated source file, so reviewers can see both the canonical language model and the multilingual design.
