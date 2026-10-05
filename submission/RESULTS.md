# Báo cáo kết quả thực thi

## Kết quả tổng hợp

- Smoke test: 9/9 bước đạt.
- Pytest: 24/24 test đạt.
- Notebook runner: 8/8 notebook đạt trong 31,8 giây ở lần kiểm tra cuối.
- Tám notebook nộp bài đã chạy đủ code cell, có output và không có error cell.

## Số đo chính

| Notebook | Bằng chứng từ lần chạy |
|---|---|
| NB1 | Bad write bị chặn bởi lỗi cast `thirty` sang Int64; Delta log, schema merge và 2 nhóm tier đều đạt. |
| NB2 | 200 → 55 file; speedup 8,3×; pruning 55×, chỉ 1/55 file có thể chứa `user_id=4242`. |
| NB3 | MERGE 100K dòng trong 0,07 giây; history có 5 version gồm RESTORE; `score < 0` còn 0 dòng. |
| NB4 | Bronze 200.000, Silver 190.052, loại 9.948 bản trùng; Gold có 8 ngày × 3 model = 24 dòng. Toàn bộ `p50 ≤ p95`; chi phí nhỏ nhất 13,4966384 USD; error rate trong [0,04217; 0,06184]. |
| NB5 | Hidden-partition pruning 10×; rename giữ `field_id=4`; data file có hai spec ID [1, 2] và vẫn đọc đủ. |
| NB6 | Delta 200 → 11 file (trên 18×); skip rate 90%; vacuum thu hồi 16,1 MB; xóa 3 orphan; Iceberg 20 → 3 snapshot; checkpoint được tạo. |
| NB7 | Random-read amplification 200×; int8 nhỏ hơn 5,8×; recall@10 = 0,904; topic fidelity = 1,000; lakehouse có 0 stale hit nhưng external index có 8; CDF phát 8 delete. |
| NB8 | Silver có 1.578 step; replay version pin khớp 1.578 step; 5 turn chỉ 1 catalog read; destructive call trả `input_required`; `user_007` giảm 8 → 0 dòng. |

## Kết luận

Các ngưỡng bắt buộc trong rubric đều được đối chiếu bằng output thực tế.
Riêng các giới hạn của NB8 được trình bày đúng là mô phỏng offline, không
diễn giải thành cơ chế authorization hay kết luận tuân thủ pháp lý.

## Bonus

Đã hoàn thành Topic D tại `submission/bonus/ARCHITECTURE.md`: 2.498 từ,
problem statement 138 từ, một sơ đồ kiến trúc, 7 quyết định với 14
alternative bị loại, 5 failure mode, phép tính storage/compute và MVP 7 ngày.
