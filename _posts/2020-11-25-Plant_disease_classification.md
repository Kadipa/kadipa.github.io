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

![Plant Dataset](https://github.com/Kadipa/kadipa.github.io/blob/master/images/1.png)
Dataset ရှိတဲ့ directory ကနေ လှမ်းဖတ်ပြီး array တခုထဲ ထည့်လိုက်ပါမယ်။ Data ကို ဖတ်ပြီးရင် outputက ဒီလိုမျိုးပြပါမယ်။ Data array ရဲ့ lengthက image အားလုံးပေါင်းရဲ့ အရေအတွက်ပါ။ ၆၄၄၂ ပုံ ရှိပါတယ်။

(၂)Data ကို ပြင်ဆင်ခြင်း

Data ဖတ်လို့ပြီးရင် data arrayကို randomly shuffle လုပ်ပါမယ်။ဘာလို့လဲဆိုတော့ class အရ ပုံတွေ အစဉ်လိုက်ဖြစ်နေတော့ training set နဲ့ testing set ခွဲရင် data balance မဖြစ်မှာ စိုးလို့ပါ။ ပြီးရင် training set ၈၀ရာခိုင်နှုန်း နဲ့ testing set ၂၀ရာခိုင်နှုန်း ခွဲပါမယ်။ Training set မှာ ပုံပေါင်း၅၁၅၃ ရှိပြီး testing setမှာ ၁၂၈၉ပုံ ရှိပါတယ်။

ကိုယ့် dataset ပေါ်မူတည်ပြီး အချိုး အမျိုးမျိုးခွဲလို့ ရပါတယ်။

Prediction လုပ်ရ ပိုလွယ်ကူအောင် class labelကို one hot encoding ပုံစံ ပြောင်းပါတယ်။ One hot encoding ဆိုတာက ဥပမာအားဖြင့် class label "Healthy", "Sptoria_leaf_spot", "Spider_mites", "Target_Spot"(categorical value) ကနေ binary variable [1.0.0.0,0.1.0.0,0.0.1.0,0.0.0.1]ပုံစံ ပြောင်းလိုက်တာ ဖြစ်ပါတယ်။

(၃) Model ကို train ခြင်း

Dataကို prepareလုပ်ပြီးရင် model ကို စtrainပါမယ်။ ဒီနေရာမှာ pre-trained model ကို သုံးပြီး image classification လုပ်ပါတယ်။ ဘာလို့လဲဆိုတော့ pre-trained modelတွေက Benchmark datasetအကြီးတွေနဲ့ trained ပြီးသား weight ကို ပြန်ယူသုံးချင်လို့ပါ။ ဒါက model ကို scratch ကနေ ပြန် trainတာထက် performance ပိုကောင်းပါတယ်။

Pretrained model ကို သုံးရာတွင် fine tuning အနေနဲ့ကော feature extractor အနေနဲ့ကော datasetရဲ့ အခြေနေပေါ်မူတည်ပြီး အဆင်ပြေသလို သုံးလို့ရပါတယ်။

ရှိပြီးသား pretrained model ကို fully connected layer ၂ခု ထပ်ထည့်ပြီး train ပါတယ်။ ပထမlayerအတွက်nodeကို 512ထားလိုက်ပြီးတော့ ဒုတိယlayerမှာ classရှိသလောက် nodeကို ထားပါတယ်။ ဒီနေရာမှာတော့ class ၄ခုရှိတဲ့ အတွက် node ၄ခုပါ။

activation functionကတော့ softmaxကို သုံးပါတယ်။ multi-class classification ဖြစ်တဲ့အတွက် categorical cross entropy ကို သုံးပါမယ်။ Optimizerအနေနဲဲ့ AdaMaxကို default parameter အတိုင်း သုံးထားပါတယ်။ Epoch ၁၀ခုကို batch size ၁၆နဲ့ trainထားပါတယ်။

Generalization ပိုကောင်းအောင် ဒီမှာ online data augmentation ကို သုံးထားပါတယ်။ Data augmentationကို များသောအားဖြင့် dataset sizeပိုကြီးအောင် လုပ်ရာတွင် သုံးလေ့ရှိကြပါတယ်။ အဓိကအားဖြင့် online data augmentation နဲ့ offline data augmentation ဆိုပြီး ရှိပါတယ်။ Offline data augmentation ဆိုတာ model မ train ခင်ကတည်းက datasetကို ပိုကြီးအောင် flip, rotation, scaling စတာတွေ သုံးပြီး training sampleပိုများအောင် လုပ်တာပါ။ Testing setကိုလည်း data augmentation လုပ်လို့ရပေမဲ့ များသောအားဖြင့် training setအတွက်ပဲ လုပ်ကြပါတယ်။ Online data augmentation ဆိုတာက model trainနေတုန်း sampleကို flip,rotate, scaleအစရှိသဖြင့် random လုပ်ပြီး train တာပါ။

(၄) Model evaluation

Model train လို့ပြီးရင် model ကို evaluation လုပ်ပြီး Train F1 score နဲ့ Test F1 scoreထုတ်ကြည့်ပါမယ်။

Model train နေတုန်း overfit ဖြစ် မဖြစ် သိစေရန် modelရဲ့ loss နဲ့ accuray ကိုလည်း plot ထုတ်ကြည့်ပါမယ်။

Classတခုချင်းစီအတွက် ဘယ်လောက် မှန်မှန် predict လုပ်နိုင်လဲ သိချင်လို့ Confusion Matrix လည်း ထုတ်ကြည့်ပါမယ်။

ဒီပိုစ့် Codeအပြည့်အစုံကို ဒီမှာ ကြည့်နိုင်ပါတယ်။
https://github.com/Kadipa/Plant_diesase_classification

References

(1) https://keras.io/api/applications/

(2) https://scikit-learn.org/stable/auto_examples/model_selection/plot_confusion_matrix.html
