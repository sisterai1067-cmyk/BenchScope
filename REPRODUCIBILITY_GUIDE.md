# [BenchScope] 독립 제3자 재현성(Reproducibility) 및 반복 검증 프로토콜

본 검증은 제안된 4단계 비순환 직교 데이터 거버넌스 프레임워크(`NonCircularBenchScopeGNN`)가 독립된 제3자의 시스템에서도 동일한 수치와 통계적 유의성($n=5$ 반복 실험)을 재현하는지 확인하기 위한 표준 절차입니다.

## 1. 기준 통제 환경 (Baseline Environment Specification)
* **OS / Architecture**: Windows 10/11 (AMD64) 또는 Linux/macOS (64-bit)
* **CPU / System RAM**: 64-bit Multi-core CPU (기준: 18 Logical Cores) / 최소 8 GB 이상 (기준: 16 GB RAM)
* **연산 정밀도 (Precision)**: `CPU-Only Execution`, IEEE 754 `torch.float32` (GPU 기종 간 비결정성 편차를 원천 배제하기 위해 CPU 고정 연산 수행)
* **Python 버전**: `Python 3.11.x` (기준: `3.11.10`)

## 2. 아티팩트 무결성 기준값 (SHA-256 Checksum)
실험 전, 배포된 두 가중치 체크포인트 파일이 원본과 1비트도 다르지 않은지 아래 해시값으로 자동 검증합니다.
* `benchscope_frozen_auditor.pt` (859.6 KB)
  - SHA-256: `4798e8fbd81e38fe49daadd4d8ff1f66ff5626456b808743612b46dc515ee142`
* `benchscope_multi_v2_frozen.pt` (875.0 KB)
  - SHA-256: `bbf1c51e370333b56973c28f6adb1598cdaaaddf0c54ba5f8fd1d96cddfa79e1`

## 3. 검증자 수행 단계 (3-Step Execution)
1. **저장소 다운로드**: `git clone https://github.com/sisterai1067-cmyk/BenchScope.git` (또는 배포된 압축 파일 해제)
2. **환경 설치**: `pip install -r requirements.txt`
3. **통합 검증 스크립트 실행**: 주피터 노트북에서 아래 제공된 **[통합 검증 코드]** 셀을 실행한 뒤, 마지막에 자동 생성되는 **`reproducibility_audit_result.csv`** 파일과 화면 출력 표를 캡처하여 회신해 주세요.
