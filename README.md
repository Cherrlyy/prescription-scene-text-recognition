# 병용금기 약물 조회 서비스를 위한 처방전 이미지 OCR


## 프로젝트 소개
처방전 이미지 업로드를 통해 처방 약물 기록 및 복용 중인 일반의약품과의 상호작용을 확인함으로써 병용금기를 주의할 수 있도록 목표했습니다.
<br>해당 페이지는 처방전 이미지 내 텍스트 인식(OCR)을 통해 처방 약물 텍스트화까지 기록되어 있습니다.



## 폴더 구조
- code : 학습 데이터 생성 / 이미지 전처리 / 모델 학습 등의 코드
- doc : 발표자료 / 산출물
- model : 사용한 사전학습 모델 / 학습 후 모델
```
📦prescription-scene-text-recognition
 ┣ 📂code
 ┃ ┣ 📜character_kor.yaml.txt
 ┃ ┣ 📜generate_traindata.ipynb
 ┃ ┣ 📜img_preprocessing.ipynb
 ┃ ┗ 📜text_detection.ipynb
 ┣ 📂doc
 ┃ ┣ 📂PPT
 ┃ ┃ ┣ 📜캡스톤디자인_10주차_3조.pdf
 ┃ ┃ ┣ 📜캡스톤디자인_11주차_3조.pdf
 ┃ ┃ ┣ 📜캡스톤디자인_12주차_3조.pdf
 ┃ ┃ ┣ 📜캡스톤디자인_13주차_3조.pdf
 ┃ ┃ ┣ 📜캡스톤디자인_14주차_3조.pdf
 ┃ ┃ ┣ 📜캡스톤디자인_6주차_3조.pdf
 ┃ ┃ ┣ 📜캡스톤디자인_7주차_3조.pdf
 ┃ ┃ ┣ 📜캡스톤디자인_8주차_3조.pdf
 ┃ ┃ ┗ 📜캡스톤디자인_9주차_3조.pdf
 ┃ ┣ 📂report
 ┃ ┃ ┣ 📜3조_기술문서.pdf
 ┃ ┃ ┗ 📜3조_최종보고서.pdf
 ┣ 📂model
 ┃ ┣ 📜custom.pth
 ┃ ┗ 📜korean_g2.pth
 ┗ 📜README.md
```

## 과정

### 전처리
![002](https://github.com/user-attachments/assets/85c56f3b-8dbf-4c09-b603-70514f19a319)
- 이미지 확대 / 팽창 및 침식 / 모폴로지 연산(잡음 제거 및 빈곳 메꾸기)
- 이진화 / 블러링
- 샤프닝

### 모델링
![001](https://github.com/user-attachments/assets/f769be13-e12e-4eb8-89fa-41431be7461f)
- 학습 이미지 생성
  - [텍스트 이미지 생성 오픈소스 프로젝트](https://github.com/Belval/TextRecognitionDataGenerator)
  - 나눔글꼴 30종으로 작성된 기본, 왜곡, 기울임, 랜덤 배경, 블러 총 5개 유형의 1글자 또는 10글자 한글 이미지
  - train data 90,000 / valid data 9,000 / test data 9,000 생성
- 학습 이미지 변환
  - [텍스트 이미지 생성 오픈소스 프로젝트](https://github.com/DaveLogs/TRDG2DTRB)
- 모델 학습 및 파인튜닝
  - 학습을 위해 EasyOCR과 동일한 네트워크 구조를 갖는 모델 사용
  - [OCR 모델 오픈소스 프로젝트](https://github.com/clovaai/deep-text-recognition-benchmark)
  - 이때 사용하는 pre-trained model은 EasyOCR에서 제공하는 한국어 OCR 모델(korean_g2.pth) 사용
  - [사전학습 모델 출처](https://www.jaided.ai/easyocr/modelhub/)

### 분석 결과
![image](https://github.com/user-attachments/assets/1e06d330-5c6b-48a5-9a0e-8008fb1f08f9)
![image](https://github.com/user-attachments/assets/51a600e5-9d12-4ccf-9927-77dd8012c8db)
- NAVER DEVIEW2023에서 발표한 평가 방법 [PopEval](https://arxiv.org/abs/1908.11060)에 따른 정확도 측정
- 평균 약 75~80%의 인식률


