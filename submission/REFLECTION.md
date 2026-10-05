# Reflection — Lab 19

**Tên:** Tran Van Khanh
**Cohort:** A20-K4
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set 50 câu, hybrid thắng trung bình (78,6% so với 77,8% keyword và
73,2% semantic) nhưng không thắng ở mọi lát cắt. Với câu `exact` chứa thuật
ngữ nguyên văn, BM25 đã đủ mạnh (96,7%) nên hybrid chỉ ngang bằng. Với câu
`paraphrase` thuần tiếng Việt, cả hai mode đều yếu (33,3% / 24,0%) vì embedding
bge-small-en huấn luyện tiếng Anh; hybrid không cứu được vì không có tín hiệu
tốt để gộp. Hybrid chỉ thắng rõ ở lát `mixed` (100% so với 97,0% và 98,5%) —
nơi câu hỏi vừa có từ khoá nguyên văn vừa có ý diễn đạt lại, nên RRF gộp được
hai tín hiệu bù trừ nhau.

Tôi sẽ không dùng hybrid khi truy vấn gần như toàn thuật ngữ chính xác: BM25
một mình cho chất lượng ngang mà rẻ hơn (P50 0,7ms so với 6,6ms) và chỉ phải
vận hành một index. Ngược lại, nếu nâng lên embedding đa ngữ tốt (bge-m3), câu
paraphrase sẽ do vector đảm nhiệm và hybrid trở nên thừa.

---

## Điều ngạc nhiên nhất khi làm lab này

Hybrid thua chính BM25 trên lát `paraphrase`: fusion chỉ mạnh khi cả hai
retriever đều mang tín hiệu, nó không phải phép màu bù được một embedding yếu
ngôn ngữ.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
