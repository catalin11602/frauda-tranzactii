# Sistem de Detectare a Fraudelor în Tranzacții Online

Această aplicație detectează tranzacții suspecte folosind algoritmul Isolation Forest.

## Cum funcționează

1. Încarcă un fișier CSV cu coloanele `amount` și `time`
2. Aplicația detectează tranzacțiile suspecte
3. Poți vizualiza și descărca rezultatele

## Lansare locală

```bash
pip install -r requirements.txt
streamlit run app.py

### 🧭 Pașii următori:

1. Creează un repository nou pe GitHub (ex: `frauda-tranzactii`)
2. Încarcă **cele 2 fișiere esențiale**: `app.py` și `requirements.txt`
3. (Opțional: `tranzactii.csv`, `README.md`)
4. Mergi pe [https://share.streamlit.io](https://share.streamlit.io) și completează:
   - `user/repo`: `username/frauda-tranzactii`
   - `branch`: `main`
   - `main file path`: `app.py`
