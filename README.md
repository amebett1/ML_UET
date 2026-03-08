# 📈 Hồi quy tuyến tính từ con số 0 (Linear Regression from Scratch)

Dự án này minh họa cách xây dựng một mô hình Hồi quy tuyến tính (Linear Regression) đơn giản bằng Python, sử dụng **Phương trình chuẩn (Normal Equation)** thông qua thư viện `numpy` và vẽ biểu đồ với `matplotlib`. Bài toán cụ thể là dự đoán **Cân nặng (y)** dựa trên **Chiều cao (x)**.

## 🧮 Cơ sở Toán học

Mục tiêu của Hồi quy tuyến tính là tìm ra một đường thẳng phù hợp nhất đi qua các điểm dữ liệu. Phương trình đường thẳng cơ bản có dạng:

$$y = w_0 + w_1x$$

Trong đó:
* $y$: Giá trị dự đoán (Cân nặng).
* $x$: Đặc trưng đầu vào (Chiều cao).
* $w_0$: Hệ số chặn (Bias/Intercept) - Điểm đường thẳng cắt trục tung.
* $w_1$: Hệ số góc (Weight/Slope) - Độ dốc của đường thẳng (Cứ cao thêm 1cm thì nặng thêm bao nhiêu kg).

Để tối ưu hóa việc tính toán cho nhiều điểm dữ liệu cùng lúc, chúng ta chuyển bài toán về dạng ma trận:

$$\mathbf{y} = \bar{\mathbf{X}}\mathbf{w}$$

* $\bar{\mathbf{X}}$ (Xbar): Ma trận dữ liệu đầu vào $X$ đã được ghép thêm một cột toàn số 1 ở đầu (để tính toán hệ số $w_0$).
* $\mathbf{w}$: Vector chứa các trọng số cần tìm: $\begin{bmatrix} w_0 \\ w_1 \end{bmatrix}$.

Nghiệm của bài toán (bộ trọng số tối ưu nhất) được tính toán trực tiếp thông qua **Phương trình chuẩn**:

$$\mathbf{w} = (\bar{\mathbf{X}}^T \bar{\mathbf{X}})^{-1} \bar{\mathbf{X}}^T \mathbf{y}$$

## 🚀 Các bước thực hiện trong Code

1. **Chuẩn bị dữ liệu**: Khởi tạo mảng dữ liệu chiều cao ($X$) và cân nặng ($y$) dưới dạng vector cột bằng `.T`.
2. **Tạo Xbar**: Tạo một vector cột toàn số 1 bằng `np.ones` và ghép vào bên trái ma trận $X$ bằng `np.concatenate(..., axis=1)`.
3. **Tính toán trọng số (w)**: 
    * Tính $\mathbf{A} = \bar{\mathbf{X}}^T \bar{\mathbf{X}}$ thông qua `np.dot`.
    * Tính $\mathbf{b} = \bar{\mathbf{X}}^T \mathbf{y}$.
    * Tìm $\mathbf{w}$ bằng cách dùng hàm ma trận nghịch đảo giả `np.linalg.pinv(A)` nhân với $\mathbf{b}$.
4. **Vẽ biểu đồ**: Rút trích $w_0$ và $w_1$ từ vector $\mathbf{w}$, sau đó vẽ đường thẳng dự đoán đè lên biểu đồ phân tán (scatter plot) của dữ liệu gốc.

## 💻 Mã nguồn (Python)

**Yêu cầu cài đặt:**
```bash
pip install numpy matplotlib