# 📘 jetson coral 연동

🌟 **jetson orin nano, nx에 Google Coral USB Accelerator인 Coral을 연동하여 모델 구동 과정**을 바탕으로 작성한 내용입니다.

## 📔 사전 준비 사항

- **하드웨어**
    - NVIDIA Jetson Orin Nano 개발 키트
    - Google Coral USB Accelerator (Edge TPU)
    - USB 케이블
- **소프트웨어**
    - Jetson Orin Nano에 Ubuntu 20.04 LTS 이상 설치
    - 관리자(root) 권한이 있는 계정
    - 인터넷 연결

## 🍿 환경 설정

      #패키지 목록 업데이트
      sudo apt update
      sudo apt upgrade -y

      #APT 저장소 추가
      echo "deb https://packages.cloud.google.com/apt coral-edgetpu-stable main" | sudo tee /etc/apt/sources.list.d/coral-edgetpu.list

      #GPG 키 추가
      curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

      # Edge TPU 런타임 : 표준
      sudo apt-get install libedgetpu1-std
      # Edge TPU 런타임 : 고성능
      sudo apt-get install libedgetpu1-max

      #python3-pip, tflite runtime 설치
      sudo apt install python3-pip -y
      pip3 install tflite-runtime

      #Git, 의존성 패키지 설치
      sudo apt install git libatlas-base-dev -y

      

## ✏️ 데모 코드 및 실행

      # 데모 코드 클론
      git clone https://github.com/google-coral/edgetpu.git

      # 이미지 분류 데모 실행
      cd examples/classify_image
python3 classify_image.py \
  --model ../../test_data/mobilenet_v2_1.0_224_inat_bird_quant_edgetpu.tflite \
  --labels ../../test_data/inat_bird_labels.txt \
  --input ../../test_data/parrot.jpg
      
