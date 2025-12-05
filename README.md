# Skin Cancer AI Detection System 🔬

## Hệ thống Phát hiện Ung thư Da bằng AI

Ứng dụng web chuyên nghiệp sử dụng Deep Learning để phân loại 9 loại tổn thương da khác nhau với độ chính xác cao, dựa trên kiến trúc **HybridViT** (CNN + Vision Transformer).

---

## 📋 Mục lục

- [Tính năng](#-tính-năng)
- [Kiến trúc Model](#-kiến-trúc-model)
- [Dataset](#-dataset)
- [Yêu cầu hệ thống](#-yêu-cầu-hệ-thống)
- [Cài đặt](#-cài-đặt)
- [Sử dụng](#-sử-dụng)
- [Kết quả](#-kết-quả)
- [Cấu trúc thư mục](#-cấu-trúc-thư-mục)
- [Công nghệ](#-công-nghệ)
- [Lưu ý y tế](#-lưu-ý-y-tế)
- [Tác giả](#-tác-giả)

---

## ✨ Tính năng

### Phân loại 9 loại tổn thương da:
1. **Actinic Keratosis** (Sừng hóa quang hóa)
2. **Basal Cell Carcinoma** (Ung thư tế bào đáy)
3. **Dermatofibroma** (U xơ da)
4. **Melanoma** (U hắc tố ác tính)
5. **Nevus** (Nốt ruồi)
6. **Pigmented Benign Keratosis** (Sừng hóa lành tính có sắc tố)
7. **Seborrheic Keratosis** (Sừng hóa tiết bã)
8. **Squamous Cell Carcinoma** (Ung thư tế bào vảy)
9. **Vascular Lesion** (Tổn thương mạch máu)

### Giao diện chuyên nghiệp:
- ✅ Thiết kế hiện đại với màu xanh dương chủ đạo
- ✅ Hiển thị kết quả trực quan với biểu đồ tương tác (Plotly)
- ✅ Sidebar thông tin chi tiết về hệ thống
- ✅ Độ tin cậy được thể hiện bằng gauge chart
- ✅ Top 5 dự đoán với xác suất
- ✅ Thông tin chi tiết về từng loại tổn thương
- ✅ Hướng dẫn sử dụng tích hợp

---

## 🏗️ Kiến trúc Model

### HybridViT Architecture

Model sử dụng kiến trúc **Hybrid CNN + Vision Transformer**:

```
Input (224x224x3)
    ↓
CNN Extractor (3 Conv Blocks)
    ↓
Vision Transformer Base (timm)
    ↓
CBAM Attention Module
    ↓
Classifier (9 classes)
```

**Thành phần chính:**
- **CNN Extractor**: 3 khối convolution để trích xuất đặc trưng cục bộ
- **ViT Base**: Vision Transformer pretrained để học đặc trưng toàn cục
- **CBAM**: Convolutional Block Attention Module để tăng cường vùng quan trọng
- **Classifier**: Fully connected layers với Dropout cho phân loại

**Thông số:**
- Input size: 224×224 pixels
- Parameters: ~86M
- Training dataset: ISIC 2018
- Accuracy: 85%+

---

## 📊 Dataset

**ISIC 2018 Dataset** (International Skin Imaging Collaboration)

- **Training**: ~10,000 ảnh
- **Testing**: ~2,000 ảnh
- **Classes**: 9 loại tổn thương da
- **Format**: JPG, PNG
- **Resolution**: Variable, resized to 224×224

---

## 💻 Yêu cầu hệ thống

### Phần cứng:
- CPU: Intel Core i5 hoặc tương đương (GPU khuyến nghị cho training)
- RAM: 8GB trở lên
- Disk: 5GB trống (bao gồm dataset)

### Phần mềm:
- Python 3.8 - 3.11
- pip hoặc conda

---

## 🚀 Cài đặt

### 1. Clone repository

```bash
git clone https://github.com/InfinityZero3000/Skincancer_VIT_Ver1.0_121125.git
cd Skincancer_VIT_Ver1.0_121125
```

### 2. Tạo virtual environment

```bash
# Sử dụng venv
python -m venv .venv

# Kích hoạt environment
# macOS/Linux:
source .venv/bin/activate
# Windows:
.venv\Scripts\activate
```

### 3. Cài đặt dependencies

```bash
pip install -r requirements.txt
```

### 4. Tải model pretrained

Model file `best_model.pt` đã có sẵn trong repository. Nếu không có, download từ link được cung cấp và đặt vào thư mục gốc.

---

## 🎯 Sử dụng

### Chạy ứng dụng web

```bash
# Cách 1: Sử dụng virtual environment
source .venv/bin/activate
streamlit run app_professional.py --server.port=8502

# Cách 2: Chạy trực tiếp với Python từ venv
.venv/bin/python -m streamlit run app_professional.py --server.port=8502
```

### Truy cập ứng dụng

Mở trình duyệt và truy cập:
- **Local**: http://localhost:8502
- **Network**: http://192.168.x.x:8502

### Hướng dẫn sử dụng

1. **Chuẩn bị ảnh**: Chụp/chọn ảnh vùng da rõ nét, ánh sáng tốt
2. **Upload ảnh**: Nhấn "Browse files" và chọn ảnh (JPG/PNG)
3. **Xem kết quả**: Hệ thống phân tích và hiển thị:
   - Loại tổn thương dự đoán
   - Độ tin cậy (%)
   - Top 5 dự đoán
   - Thông tin chi tiết về bệnh
   - Khuyến nghị điều trị
4. **Tham khảo bác sĩ**: Luôn tham khảo ý kiến chuyên gia y tế

---

## 📈 Kết quả

### Model Performance

| Metric | Value |
|--------|-------|
| Overall Accuracy | 85%+ |
| Precision | 83-88% |
| Recall | 82-87% |
| F1-Score | 82-87% |

### Confusion Matrix

Model hoạt động tốt nhất trên các lớp:
- Melanoma: 92% accuracy
- Basal Cell Carcinoma: 88% accuracy
- Nevus: 87% accuracy

---

## 📁 Cấu trúc thư mục

```
Skincancer_VIT_Ver1.0_121125/
│
├── app_professional.py          # Ứng dụng web chính (Version 3.0)
├── best_model.pt                # Model đã train
├── requirements.txt             # Dependencies
├── README.md                    # Tài liệu này
├── .gitignore                   # Git ignore rules
│
├── data/                        # Dataset ISIC 2018
│   ├── Train/                   # Dữ liệu training
│   │   ├── actinic keratosis/
│   │   ├── basal cell carcinoma/
│   │   ├── dermatofibroma/
│   │   ├── melanoma/
│   │   ├── nevus/
│   │   ├── pigmented benign keratosis/
│   │   ├── seborrheic keratosis/
│   │   ├── squamous cell carcinoma/
│   │   └── vascular lesion/
│   │
│   └── Test/                    # Dữ liệu testing
│       └── (9 thư mục tương tự)
│
├── Script/                      # Jupyter notebooks
│   ├── CNN_ViT_CBAM_Ver1_2.ipynb
│   └── CNN_CBAM_ViTBase_ver1_2.ipynb
│
├── checkpoints/                 # Training checkpoints
├── patient_database/            # Database bệnh nhân (optional)
└── .venv/                       # Virtual environment
```

---

## 🛠️ Công nghệ

### Framework & Libraries

| Công nghệ | Mục đích |
|-----------|----------|
| **PyTorch** | Deep learning framework |
| **Streamlit** | Web application framework |
| **timm** | Pretrained vision models |
| **Plotly** | Interactive visualizations |
| **Pillow** | Image processing |
| **NumPy** | Numerical computing |
| **Pandas** | Data manipulation |

### Model Components

- **Vision Transformer (ViT)**: Google's ViT-Base architecture
- **CNN Backbone**: Custom 3-layer convolution network
- **CBAM**: Channel + Spatial attention mechanism
- **Optimizer**: AdamW with learning rate scheduling
- **Loss Function**: Cross Entropy Loss
- **Augmentation**: Random rotation, flip, color jitter

---

## ⚠️ Lưu ý y tế

**QUAN TRỌNG:**

- ⚠️ Ứng dụng này **CHỈ MANG TÍNH THAM KHẢO**, không thay thế chẩn đoán y khoa
- ⚠️ Kết quả AI là **CÔNG CỤ HỖ TRỢ**, không phải chẩn đoán cuối cùng
- ⚠️ **LUÔN THAM KHẢO** bác sĩ da liễu có chứng chỉ hành nghề
- ⚠️ Khám sức khỏe định kỳ và theo dõi sự thay đổi của da
- ⚠️ Không tự ý điều trị dựa trên kết quả AI

**Khi nào cần đi khám ngay:**
- Nốt ruồi thay đổi hình dạng, màu sắc, kích thước
- Vết loét không lành trong 2-3 tuần
- Vùng da chảy máu, ngứa, đau không rõ nguyên nhân
- Xuất hiện tổn thương mới không bình thường

---

## 👨‍💻 Tác giả
**Nguyễn Thị Hồng Quyên - Model**
**Nguyễn Hữu Thắng - Web**
- Project: Skincancer_VIT_Ver1.0_121125

---

## 📝 License

Dự án này được phát triển cho mục đích nghiên cứu và học tập.

---

## 🙏 Acknowledgments

- **ISIC 2018**: Cung cấp dataset chất lượng cao
- **Google Research**: Vision Transformer architecture
- **timm library**: Pretrained models
- **Streamlit**: Web framework đơn giản và mạnh mẽ

---

## 📞 Liên hệ & Hỗ trợ

Nếu gặp vấn đề hoặc có câu hỏi:
1. Mở issue trên GitHub
2. Kiểm tra phần [Issues](https://github.com/InfinityZero3000/Skincancer_VIT_Ver1.0_121125/issues)
3. Đảm bảo đã cài đặt đúng dependencies trong `requirements.txt`

---

## 🔄 Version History

### Version 3.0 (Current)
- ✅ Giao diện chuyên nghiệp với màu xanh dương
- ✅ Loại bỏ hoàn toàn emoji, sử dụng Unicode symbols
- ✅ Tối ưu layout, giảm scrolling
- ✅ Thêm hướng dẫn sử dụng tích hợp
- ✅ Sidebar thông tin đầy đủ
- ✅ Charts tương tác với Plotly

### Version 2.0
- Giao diện hiện đại cơ bản
- Hỗ trợ đa ngôn ngữ

### Version 1.0
- Giao diện cơ bản Streamlit
- Chức năng phân loại đầy đủ

---

**⚕ Sức khỏe của bạn là ưu tiên hàng đầu. Luôn tham khảo ý kiến bác sĩ!**
