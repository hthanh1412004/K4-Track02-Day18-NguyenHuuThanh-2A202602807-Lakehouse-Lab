# Reflection

Anti-pattern tôi thấy dễ gặp nhất là coi external vector index như nguồn dữ liệu
chính. Trong hệ thống RAG tôi quan tâm, document có thể bị sửa, hết quyền sử dụng
hoặc phải xóa theo yêu cầu của chủ thể. Nếu pipeline chỉ upsert embedding mà không
truyền delete, index cũ vẫn trả về nội dung không còn tồn tại trong lakehouse.

Tôi sẽ giữ Delta/Iceberg là system of record, pin version cho mỗi lần build index và
coi index là derived state có thể tái tạo. Consumer phải xử lý idempotent cả insert,
update và delete từ CDF, ghi checkpoint, theo dõi lag và đối soát định kỳ với
snapshot nguồn. Bảng dữ liệu cũng cần retention phù hợp để xóa vật lý sau khi
reader hết thời gian an toàn.

Tôi dùng OpenAI Codex để hỗ trợ đọc yêu cầu, chạy kiểm tra và hỗ trợ biên tập
báo cáo; phạm vi chi tiết được ghi trong `AI_USAGE.md`.
