```
WHITESPACE = _{ " " | "," | "\t" | NEWLINE }
COMMENT = _{ comment_line | comment_block }

comment_line = { ";" ~ (!NEWLINE ~ ANY)* }
comment_block = { "_(" ~ (form | comment_line | comment_block)* ~ ")" }

program = _{ form* }
form = _{ atom | sexp | tuple | vector | record }

atom = _{ keyword | symbol | character | string | float | integer | rest_param }
sexp = { "(" ~ form* ~ ")" }
tuple = { "[" ~ form* ~ "]" }
vector = { "{" ~ form* ~ "}" }
record = { "#{" ~ (record_pair)* ~ "}" }
record_pair = { keyword ~ form }

keyword = @{ ":" ~ symbol }
symbol = @{ "@"? ~ symbol_head ~ symbol_rest* }
character = @{ "\\" ~ (alpha_num)+ }
string = @{ "\"" ~ (!"\"" ~ ANY)* ~ "\"" }
float = @{ "~"? ~ integer? ~ "." ~ integer? }
integer = @{ "~"? ~ digit+ }
rest_param = { "&" }

symbol_head = { alpha | "!" | "?" | "*" | "-" | "=" | "+" | ":" | ">" | "_" }
symbol_rest = { "/" | symbol_head | digit }
alpha_num = { alpha | digit }
alpha = { 'a'..'z' | 'A'..'Z' | "-" }
digit = { '0'..'9' }
```
