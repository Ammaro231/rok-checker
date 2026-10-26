import streamlit as st
import requests

st.title("RoK Resources Checker 💰")

player_id = st.text_input("أدخل رقم الـ ID الخاص باللاعب:")

if st.button("جلب الموارد"):
    if player_id:
        # هنا تضع الرابط الحقيقي الذي يستقبل بيانات الحساب
        url = "https://lilith.com" 
        payload = {"uid": player_id, "game_id": "rok"}

        try:
            response = requests.post(url, json=payload)
            if response.status_code == 200:
                data = response.json()
                # عرض البيانات للمستخدم بشكل منسق
                st.success("تم جلب البيانات بنجاح!")
                st.write(data) 
            else:
                st.error("فشل الاتصال بسيرفر اللعبة")
        except:
            st.error("حدث خطأ أثناء جلب البيانات")
    else:
        st.warning("الرجاء إدخال الـ ID أولاً")
