---
title: 'Plant Disease Classification Using Convolutional Neural Networks(CNN)'
date: 2020-11-25
permalink: /posts/2020/11/plant_disese_classification/
tags:
  - Plant Disease 
  - Classification
  - CNN
---

အခုနောက်ပိုင်းမှာ domain မျိုးစုံအတွက် image classificationလုပ်ရာတွင်CNNကို အများဆုံး အသုံးပြုလာကြပါတယ်။ Image classification ဆိုတာနဲ့ CNN ကို ပြေးမြင်ရလောက်တဲ့ အထိပါပဲ။ ဒီပို့စ်မှာတော့ agricultural domain အတွက် plant disease classification ကို CNN သုံးပြီး ဘယ်လို လုပ်မလဲဆိုတာ ပြန်လည်မျှဝေချင်ပါတယ်။ Pretrained CNN model ကို သုံးပြီး ကိုယ့် Dataကို ဘယ်လို trainမလဲ ဆိုတာရှင်းပြချင်ပါတယ်။


(၁) Data ဖတ်ခြင်း


ပထမဦးစွာ datasetအကြောင်း ပြောချင်ပါတယ်။ PlantVillage datasetဆိုတာက အပင်မျိုးစုံရဲ့ disease တော်တော်များများကို စုထားတဲ့ datasetကြီး ဖြစ်ပါတယ်။Dataset ကို https://github.com/spMohanty/PlantVillage-Dataset/tree/master/raw/color ကနေDown လို့ ရပါတယ်။

ဒီပို့စ်မှာတော့ PlantVillage datasetကြီးထဲကမှ tomato ပတ်သက်တဲ့ class ၄ခုကို ထုတ်ပြီး စမ်းပြချင်ပါတယ်။ "Healthy" classရယ် "Sptoria_leaf_spot", "Spider_mites", "Target_Spot"ဆိုတဲ့ disease ၃မျိုးရယ် ထုတ်ပြီး Label ၄ခုအတွက် plant disease classification လုပ်ပြမှာပါ။
Datasetပုံစံက ဒီလိုမျိုး ရှိတာပါ။
