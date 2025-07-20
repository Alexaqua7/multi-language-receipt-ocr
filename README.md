# 🧾 Multilingual Receipt OCR

카메라로 영수증을 인식할 경우 자동으로 영수증 내용이 입력되는 어플리케이션이 있습니다.  
이처럼 OCR (Optical Character Recognition) 기술은 사람이 직접 쓰거나 이미지 속에 있는 문자를 얻은 다음 이를 컴퓨터가 인식할 수 있도록 하는 기술로, 컴퓨터 비전 분야에서 현재 널리 쓰이는 대표적인 기술 중 하나입니다.

OCR은 글자 검출 (text detection), 글자 인식 (text recognition), 정렬기 (Serializer) 등의 모듈로 이루어져 있으며,  
본 대회에서는 다국어 (중국어, 일본어, 태국어, 베트남어)로 작성된 영수증 이미지에 대한 **글자 검출(Task 1)** 만을 수행합니다.

---

## 🏆 Result

- **Public Score**: `0.9030`  
- **Private Score**: `0.8983`

📄 [Wrap-up Report 보기](https://github.com/user-attachments/files/17736758/level2_CV.3_CV_.04.docx.pdf)

---

## 📦 Data

- AI Stage 제공 다국어 영수증 데이터셋 사용
- 각 언어별로 100장씩 총 **400장의 학습 이미지**와 UFO 형식의 라벨 파일 제공
- Test 데이터셋 포함 (레이블 없음)

데이터 디렉토리 구조는 다음과 같습니다:

```
data/
├── chinese_receipt/
├── japanese_receipt/
├── thai_receipt/
├── vietnamese_receipt/
├── merged_receipts/
```
> 📏 **Evaluation Metric**: `f1 Score`
---

## 👥 팀원 소개

<table>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/7c44b0c5-927a-4c65-8d21-8e240bcf1618" width="150px;" alt="강대민"/><br />
      <b>강대민 (팀장)</b><br />
      실험 환경 구성, <br />
      전처리 실험,<br />
      Streamlit 페이지 개발, EasyOCR 라벨 검수,<br />
      Ensemble 최종 진행 및 발표 총괄
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/fc431d0d-51d5-4774-b900-67bc6a2bb2b5" width="150px;" alt="김홍주"/><br />
      <b>김홍주</b><br />
      Optuna 기능 개발, <br />
      Super Resolution 적용, <br />
      Text Masking 데이터로 Fine-tuning
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/ddebfbe1-317d-4bf7-915c-524e51e5bd69" width="150px;" alt="박나영"/><br />
      <b>박나영</b><br />
      Stable Diffusion XL-refiner 1.0 활용<br />
      합성 영수증 데이터 제작
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/b17ce868-5498-4acf-8831-31829f8f7cbd" width="150px;" alt="서승환"/><br />
      <b>서승환</b><br />
      Stable Diffusion 3.5 Large 활용,<br />
      합성 영수증 이미지 생성 및 CV 기반 전처리
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/d155ec79-8d03-45d4-b703-44a848b9b463" width="150px;" alt="이종서"/><br />
      <b>이종서</b><br />
      SROIE2019 외부 데이터셋 활용,<br />
      최종 Ensemble 전략 설계 및 적용
    </td>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/9a15231a-b69d-447f-9070-f58b29ccdcec" width="150px;" alt="이한성"/><br />
      <b>이한성</b><br />
      CORD, WildReceipt 외부 데이터셋 구축,<br />
      외부 데이터 학습 및 Base Fine-tuning
    </td>
  </tr>
</table>

---

## 🧠 Model

- 사용 모델: [**EAST** (Efficient and Accurate Scene Text Detector)](https://arxiv.org/abs/1704.03155)
- 대회 규정 상 **단일 모델만 사용** (Ensemble 또는 다른 모델 불가)

---

## 🔧 Usage

### Installation

```bash
git clone https://github.com/boostcampaitech7/level2-datacentric-cv-04.git
cd level2-datacentric-cv-04
chmod +x server_setting.sh
./server_setting.sh
```

### Training

```bash
python train.py --data_dir=./data --model_dir=./trained_models --image_size=2048 --input_size=1024 --batch_size=8 --learning_rate=1e-3 --max_epoch=100
```

### Inference

```bash
python inference.py --data_dir=./data --output_dir --input_size=2048 --batch_size=8
```

---

## 📁 Project Structure

```plaintext
level2-datacentric-cv-04/
├── data/
├── streamlit/
├── utils/
├── pths/
├── predictions/
├── trained_models/
├── dataset.py
├── deteval.py
├── east_dataset.py
├── train.py
├── inference.py
├── requirements.txt
├── loss.py
├── model.py
├── detect.py
└── README.md
```
