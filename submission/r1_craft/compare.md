# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_270517.jpg
- L7 mid IGNORE_SCOPE
## adasind_271039.jpg
- L12 center IGNORE_SCOPE
- L1 center SPURIOUS
- L2 mid SPURIOUS
- L3+R6 mid WRONG_CLASS
- L11 center SPURIOUS
- R10 center MISSING
## adasind_295948.jpg
- L5 mid IGNORE_SCOPE
- L6 mid IGNORE_SCOPE
- L7 mid IGNORE_SCOPE
- L8 mid IGNORE_SCOPE
- L9 mid IGNORE_SCOPE
- L10 mid IGNORE_SCOPE
- L11 mid IGNORE_SCOPE
- L2+R1 center WRONG_CLASS
- L3 center SPURIOUS
- L4+R3 mid WRONG_CLASS
- L12 edge SPURIOUS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 12 | 10 | 2 | 4 |
| mid | 5 | 3 | 2 | 3 |
| edge | 3 | 3 | 0 | 1 |
