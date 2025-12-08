## 📁 폴더 구조 (현재 기준)

- `data/`
  - `raw/`  
    - 원본 이미지(`train_images/`), json annotation(`train_annotations/`) 폴더
  - `processed/`  
    - `matched_pairs.csv` : 이미지–JSON 1:1 매칭 결과  
    - `train_labels.csv` : 학습용 라벨(경로, bbox, 라벨명 등) 정리본
- `src/`
  - `data_pipeline.py`
  - `pill_dataset.py`
  - `test_pipeline.py`
- `venv/` : 가상환경

---

## 1. `data_pipeline.py`

원본 AI Hub 데이터(`/data/raw`)에서 **이미지–JSON 매칭 + 라벨/박스 정보 정리**해서  
`data/processed/train_labels.csv`를 만드는 스크립트.

### 주요 기능

- `train_images` / `train_annotations` 폴더를 훑어서
  - 이미지 파일 경로
  - 대응되는 JSON 경로
  - JSON 안의 **알약 이름(label)**, **bbox(x, y, w, h)**  
  - 이미지 `width`, `height`, JSON 최상위 key 정보  
  를 한 줄에 묶어서 CSV로 저장
- 이상한 샘플(경로 깨짐, JSON 없는 이미지 등)은 로그만 남기고 스킵

### 실행 방법

프로젝트 루트에서:

```bash
# 가상환경 활성화된 상태라고 가정
python src/data_pipeline.py
