# Chapter 11: Phân tích phương sai (ANOVA)

## Core Idea
So sánh giá trị trung bình giữa nhiều nhóm (từ 3 nhóm trở lên) để xác định xem có sự khác biệt có ý nghĩa thống kê hay không.

## Frameworks Introduced
- **One-way ANOVA**: So sánh theo một yếu tố phân loại (ví dụ: loại bệnh).
- **Two-way ANOVA**: So sánh theo hai yếu tố đồng thời (ví dụ: loại vật liệu và điều kiện thí nghiệm).
- **Multiple Comparisons**: Điều chỉnh trị số p khi thực hiện nhiều so sánh cặp để tránh sai số loại I.

## Key Concepts
- **`aov()`**: Hàm phân tích phương sai.
- **`anova(lm_object)`**: Hiển thị bảng ANOVA từ một mô hình tuyến tính.
- **F-value**: Tỉ số giữa biến thiên giữa các nhóm và biến thiên trong nội bộ nhóm.
- **Bonferroni / Tukey HSD**: Các phương pháp điều chỉnh p-value cho so sánh nhiều nhóm.
- **`kruskal.test()`**: Kiểm định phi tham số tương đương với ANOVA (khi dữ liệu không chuẩn).

## Mental Models
- **Variation Breakdown**: ANOVA chia tổng biến thiên của dữ liệu thành biến thiên do yếu tố đang xét và biến thiên ngẫu nhiên (phần dư).

## Code Examples
```r
# 1. ANOVA một chiều
group <- as.factor(group) # Phải chuyển sang factor
fit <- lm(galactose ~ group)
anova(fit)

# 2. So sánh cặp (Tukey HSD)
res <- aov(galactose ~ group)
TukeyHSD(res)

# 3. Điều chỉnh Bonferroni
pairwise.t.test(galactose, group, p.adj="bonferroni")

# 4. ANOVA hai chiều
twoway <- lm(score ~ condition + material)
anova(twoway)

# 5. Kiểm định phi tham số
kruskal.test(galactose ~ group)
```

## Worked Example
**So sánh độ galactose giữa 3 nhóm bệnh (Crohn, Viêm ruột, Đối chứng):**
```r
# Phân tích
fit <- lm(galactose ~ group)
anova(fit)
# Nếu p < 0.05, ta chạy Tukey để xem nhóm nào khác nhóm nào:
TukeyHSD(aov(galactose ~ group))
# Kết quả sẽ cho thấy sai biệt trung bình và khoảng tin cậy 95% giữa từng cặp.
```

## Key Takeaways
1. Biến nhóm bắt buộc phải là `factor`.
2. ANOVA chỉ cho biết "có sự khác biệt", còn Tukey mới cho biết "khác biệt ở đâu".
3. Dùng `kruskal.test` nếu dữ liệu có quá nhiều giá trị ngoại biên hoặc không phân phối chuẩn.

## Connects To
- **Ch 9**: ANOVA là sự mở rộng của t-test.
- **Ch 13**: Ước tính cỡ mẫu cho thiết kế ANOVA.
