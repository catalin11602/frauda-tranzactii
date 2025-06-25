import streamlit as st
import pandas as pd
from sklearn.ensemble import IsolationForest
import matplotlib.pyplot as plt
import seaborn as sns

st.title("🕵️‍♂️ Sistem de Detectare a Fraudelor în Tranzacții Online")
st.markdown("Încarcă un fișier CSV care conține tranzacții (ex: `amount`, `time`)")

uploaded_file = st.file_uploader("Încarcă fișierul CSV", type=["csv"])

if uploaded_file is not None:
    df = pd.read_csv(uploaded_file)

    if 'amount' not in df.columns or 'time' not in df.columns:
        st.error("Fișierul trebuie să conțină coloanele: 'amount' și 'time'")
    else:
        st.success("Fișier încărcat cu succes!")
        st.subheader("📄 Date brute")
        st.write(df)

        features = df[['amount', 'time']]
        model = IsolationForest(n_estimators=100, contamination=0.1, random_state=42)
        df['fraud_predict'] = model.fit_predict(features)
        df['fraud_predict'] = df['fraud_predict'].map({1: 0, -1: 1})
        df['status'] = df['fraud_predict'].map({0: 'Normal', 1: 'Fraudă'})

        st.subheader("🔍 Rezultate detecție")
        st.dataframe(df)

        total_fraude = df['fraud_predict'].sum()
        st.info(f"⚠️ Tranzacții suspecte detectate: {total_fraude}")

        st.subheader("📊 Vizualizare")
        fig, ax = plt.subplots()
        sns.scatterplot(data=df, x="amount", y="time", hue="status", palette={"Normal": "green", "Fraudă": "red"}, ax=ax)
        st.pyplot(fig)

        csv_output = df.to_csv(index=False).encode('utf-8')
        st.download_button("📥 Descarcă rezultatele", data=csv_output, file_name='rezultate_frauda.csv', mime='text/csv')
