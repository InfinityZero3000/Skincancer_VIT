# Deploy to Streamlit Community Cloud

## Hướng dẫn Deploy

### Bước 1: Chuẩn bị Git LFS cho file model lớn

File `best_model.pt` (330MB) vượt quá giới hạn GitHub (100MB), cần dùng Git LFS:

```bash
# Cài đặt Git LFS (nếu chưa có)
brew install git-lfs  # macOS
# hoặc: sudo apt-get install git-lfs  # Linux

# Khởi tạo Git LFS
git lfs install

# Track file model
git lfs track "*.pt"

# Add .gitattributes
git add .gitattributes

# Commit
git add best_model.pt
git commit -m "Add model with Git LFS"
git push origin main
```

### Bước 2: Push code lên GitHub

```bash
# Add tất cả file đã thay đổi
git add .

# Commit
git commit -m "Ready for deployment - Professional UI with flowchart"

# Push lên GitHub
git push origin main
```

### Bước 3: Deploy trên Streamlit Community Cloud

1. **Truy cập**: https://share.streamlit.io/
2. **Đăng nhập** bằng GitHub
3. **New app** → Chọn repository: `InfinityZero3000/Skincancer_VIT_Ver1.0_121125`
4. **Main file path**: `app_professional.py`
5. **Deploy!**

---

## Lưu ý quan trọng

### File model quá lớn
- GitHub free: Max 100MB/file
- Git LFS free: Max 1GB storage, 1GB bandwidth/month
- **Giải pháp thay thế**:
  - Upload model lên Google Drive/Dropbox
  - Download model khi app khởi động
  - Hoặc dùng Hugging Face Model Hub

### Code tải model từ URL (Nếu không dùng Git LFS)

```python
import os
import gdown

CHECKPOINT_PATH = "best_model.pt"
MODEL_URL = "YOUR_GOOGLE_DRIVE_LINK"  # Share link từ Google Drive

if not os.path.exists(CHECKPOINT_PATH):
    gdown.download(MODEL_URL, CHECKPOINT_PATH, quiet=False, fuzzy=True)
```

Thêm vào requirements.txt:
```
gdown>=4.7.1
```

---

## Cấu hình đã tạo

✅ **requirements.txt** - Updated với đúng version
✅ **.streamlit/config.toml** - Theme xanh dương
✅ **README.md** - Hướng dẫn đầy đủ
✅ **.gitignore** - Loại trừ file không cần

---

## Deploy thay thế

### Option 2: Hugging Face Spaces
```bash
# Tạo Space mới tại: https://huggingface.co/spaces
# Clone và push code
git clone https://huggingface.co/spaces/YOUR_USERNAME/skin-cancer-ai
cd skin-cancer-ai
cp -r /path/to/project/* .
git add .
git commit -m "Initial commit"
git push
```

### Option 3: Railway.app
1. Truy cập: https://railway.app/
2. New Project → Deploy from GitHub
3. Select repo
4. Railway tự động detect Streamlit và deploy

### Option 4: Render.com
1. Truy cập: https://render.com/
2. New → Web Service
3. Connect GitHub repo
4. Build Command: `pip install -r requirements.txt`
5. Start Command: `streamlit run app_professional.py --server.port=$PORT --server.address=0.0.0.0`

---

## URL sau khi deploy

Streamlit Cloud: `https://YOUR_USERNAME-skincancer-vit.streamlit.app`

Enjoy your deployed AI app! 🚀
