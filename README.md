# Insider Risk Early Detection & Conformal Profiling Pipeline

[![Python 3.13](https://img.shields.io/badge/python-3.13-blue.svg)](https://www.python.org/downloads/release/python-3130/)
[![Package Manager: uv](https://img.shields.io/badge/managed%20by-uv-orange.svg)](https://github.com/astral-sh/uv)
[![Code Style: Ruff](https://img.shields.io/badge/code%20style-ruff-000000.svg)](https://github.com/astral-sh/ruff)
[![Dataset: CERT r4.2](https://img.shields.io/badge/benchmark-CERT%20r4.2-brightgreen.svg)](https://kilthub.cmu.edu/articles/dataset/Insider_Threat_Test_Dataset/12841247)

Программный прототип метода предиктивного обнаружения инсайдерских угроз на основе потокового психолингвистического риск-скрининга корпоративных коммуникаций, защищенного динамического профилирования и гипотезно-ориентированного аудита системной телеметрии.

---

Предложенное решение обеспечивает компромисс между временем упреждения инцидента ($T_{\text{lead}}$ до 246 суток) и строгим ограничением ложных тревог, исключая самонормализацию эталона.

---

## Быстрый старт

### Требования
- Python `>= 3.13`
- Пакетный менеджер [`uv`](https://docs.astral.sh/uv/)

### Установка

```bash
git clone [https://github.com/your-username/insider-risk-detection.git](https://github.com/your-username/insider-risk-detection.git)
cd insider-risk-detection

# Синхронизация зависимостей
uv sync

# Загрузка языковой модели spaCy
uv run python -m spacy download en_core_web_sm
```

### Запуск экспериментов

1. **Запуск оценки на сценариях CERT r4.2:**
   *(Требуется наличие распакованных логов датасета в папке `archive/`)*
   ```bash
   # Инсайдер 1 сценария (AAM0658)
   uv run python main.py --dataset --user aam0658

   # Инсайдер 2 сценария (AAF0535)
   uv run python main.py --dataset --user aaf0535

   # Инсайдер 3 сценария (CSC0217)
   uv run python main.py --dataset --user csc0217
   ```

2. **Запуск стресс-тестирования на медленный дрейф (Slow Ramp Drift):**
   ```bash
   uv run python run_stress_test.py
   ```

Все сформированные отчеты (`incident_report.md`, `baseline_comparison.md`) и графики сохраняются в директорию `output/`.
