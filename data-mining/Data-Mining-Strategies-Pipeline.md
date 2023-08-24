### Data Mining Strategies and Pipeline

ကျွန်တော်တို့ Generative AI တွေ powerful ဖြစ်လာတော့ Machine Learning ဖက်ကို explore လုပ်ကြည့်ချင်တယ်။
ရှိပြီးသား Product မှာ AI ပက်သက်တဲ့ features တွေ introduce လုပ်ချင်တယ်။ ဒီအရွေ့မှာ adapt လုပ်ချင်ကြတဲ့သူတွေရှိမှာပါ။

ဘယ်လိုပဲ ဆိုဆို ကိုယ်က Machine Learning, Deep Learning area ထဲကို စပြီး explore လုပ်တော့မယ် ဆိုရင်၊
ကိုယ့်မှာရှိပြီးသား Product data တွေကို analyze လုပ်တော့မယ်ဆိုရင် ရှိပြီးသား ကိုယ်လုပ်ချင်တဲ့ use case နဲ့ကိုက်အောင် အဆင့်ဆင့် ပြောင်းယူရတယ်။

မလိုတဲ့ data တွေ ဖယ်ပစ်ရတယ်၊ ဘယ်လို data အမျိုးအစား တွေတော့ ကောင်းကောင်း အသုံးချလို့ရမယ်။
ဘယ်ဟာတွေကတော့ good to have ဆိုတာမျိုးပေါ့။ နောက်လိုအပ်ရင် data transformation လုပ်ရတာတွေရှိမယ်။
ဒီကနေမှ ထွက်လာတဲ့ data တွေကို ML algorithm/training process တွေမှာ ပြန်သုံးလို့ရအောင် data modeling လုပ်ရမှာတွေ ရှိတယ်။

ဒီ process တွေကို Data Mining လုပ်တယ်လို့ ပြောလို့ရတယ်။ Data Mining process မှာ ဘာတွေပါရမလဲ။ ဘယ်လို strategy တွေ သုံးလို့ရလဲ။
နောက် နေရာအသီးသီးကနေ ရလာတဲ့ data တွေကို သုံးလို့ usable ဖြစ်တဲ့အထိ mining လုပ်တဲ့ pipeline တစ်ခု ဘယ်လို တည်ဆောက်ကြမလဲ။

Understanding your data

ပထမဆုံး ဘာမှမလုပ်ခင် ကိုယ့် data ရဲ့ nature ကို နားလည်အောင် လုပ်ဖို့လိုတယ်။
ဒီအတွက် data နဲ့ ပက်သက်တဲ့ domain knowledge လည်းရှိဖို့ လိုတာပေါ့။ 

အဓိက အားဖြင့် ဘယ်လို data အမျိုးအစားတွေပါလဲ။ numeric value လား၊ အမျိုးအစား နှစ်မျိုး သုံးမျိုး ခွဲလို့ရတဲ့ categorical value လား။

numeric value မှာဆိုရင်လည်း ဖြစ်နိုင်ချေ အများကြီးရှိတဲ့ continuous value လား။
ဥပမာ အတန်းတစ်တန်းထဲမှာ ကျောင်းသား ဘယ်နှစ်ယောက်ရှိလဲဆိုရင် 30.5 လို့ သွားပြောလို့ မရဘူး။ ဒါမျိုးကိုကျ discrete value လို့ခေါ်တယ်။ Order, ranking တွေပါတဲ့ ကောင်မျိုးလား။
နောက် interval value တွေဆိုရင် scale တစ်ခုခုရှိမယ်၊ ဒါပေမဲ့ true zero မရှိဘူး။ ဆိုပါစို့ temperature 0C လို့ပြောတာသည် temperature မရှိဘူးလို့ ပြောတာ မဟုတ်ဘူး။

categorical မှာကျတော့ nominal နဲ့ ordinal values ဆိုပြီး နှစ်မျိုးခွဲလို့ရတဘ်။ 
အင်္ကျီ size - small, medium, or large ဒါဆိုရင် order တော့ရှိတယ် ဘယ်လောက် အတိုင်းအတာလဲဆိုတာမျိုး အတိအကျ ပြောလို့မရဘူး။
ဒါမျိုးကို Ordinal လို့ သုံးတယ်။ အခုလို ranking လုပ်လို့မရတဲ့ categories တွေကို Nominal လို့သုံးတယ်။

တစ်ခြား data အမျိုးအစားတွေလည်း ရှိသေးတယ်၊ explore လုပ်ကြည့်ပါ။

Preprocessing

ကိုယ့်မှာ ရှိတဲ့ data ရဲ့ သဘော သဘာဝ ကိုလည်း နားလည်ပြီ ဆိုရင် စပြီးတော့ cleaning လုပ်လို့ရပြီ။
algorithm ဘယ်လောက် ကောင်းကောင်း၊ ML engineer တွေက ဘယ်လို architecture ပဲ သုံးသုံး ကိုယ့်ရဲ့ data က garbage ဖြစ်နေရင် ရလာတဲ့ result သည်လည်း ကောင်းမှာ မဟုတ်ဘူး။

missing values ဖြစ်နေတဲ့ value တွေကို ဘယ်လို handle လုပ်မလဲ။ တစ်ချို့ features တွေမှာ missing ဖြစ်နေတဲ့ value တွေ တအားများရင် သူတို့ကို ဖယ်ပစ်လို့ ရတယ်။
threshold တစ်ခုထားပေါ့။ ဥပမာ 100K samples ရှိမယ်၊ missing value က 10% ထက်များရင် ဒီ feature ကိုမသုံးတော့ဘူး ဆိုတာမျိုး။ 
5% threshold က တော်တော်များများ feature တွေအတွက် standard ပါ။ 5% အောက်နည်းရင် ဘာလုပ်ကြမလဲ။

numerical values တွေဆိုရင် mean, median, mode စတဲ့ value တွေ သုံးပြီးတော့ missing ဖြစ်နေတဲ့နေရာမှာ အစားထိုးလို့ရတယ်။ feature ပေါ်မူတည်ပြိး ဘယ်ဟာက သင့်တော်မယ်
လို့ ဆုံးဖြတ်ဖို့လိုတယ်။ တစ်ခြား heuristic တွေ သုံးပြီး value ကို estimate လုပ်လည်းရတယ်။ imputation လို့ခေါ်တယ်။

categorical values တွေဆိုရင် empty category လိုမျိုး ယူဆလိုက်တာ၊ အပေါ်မှာပြောခဲ့တဲ့ အထဲက mode ကိုသုံးလို့လည်း ရတယ်။ 
K-Nearest Neighbors (KNN) တို့လို algorithm သုံးပြီး similar ဖြစ်တဲ့ record တွေရှာ၊ သူတို့ရဲ့ category ကို ယူသုံးတာမျိုးလဲ လုပ်လို့ရတယ်။

တစ်ချို့ value တွေက dataset တစ်ခုလုံးကနေ ကွဲထွက်နေတာလဲ ရှိနိုင်တယ်။ model ရဲ့ performance, output quality ကိုသွားပြီး impact ဖြစ်နိုင်တယ်။ 
ဆိုတော့ ကျန်တဲ့ dataset နဲ့ နီးစပ်အောင် ပြောင်းရင်ပြောင်း ဒါမှမဟုတ် remove လုပ်ပစ်သင့်တယ်။

noise data တွေပါရင်လည်း data distribution ကို ဖျက်စီးပစ်နိုင်တယ်။ ဒီလို အခြေနေမျိုးမှာဆိုရင် distribution ကို smooth ဖြစ်သွားအောင် ဖယ်ပစ်တာ၊ transformation စသည်ဖြင့် လိုအပ်သလို
လုပ်ဖို့လိုတယ်။

Feature Engineering

ကိုယ့်ရဲ့ use case နဲ့ ကိုက်မဲ့ features တွေကို ရွေးဖို့လိုတယ်။ feature တွေ တစ်ခုနဲ့ တစ်ခု အပြန်အလှန် ဘယ်လို စပ်ဆက်နေလဲ ဆိုတာမျိုးကို correlation လိုကောင်မျိုးတွေ သုံးပြီးတော့
ထုတ်ကြည့်လို့ ရတယ်။ ဥပမာ Housing dataset ဆိုပါစို့ price - living square_ft relation သည် price to bathroom ထက်စာရင် ပိုပြီး သဘာဝ ကျတယ်။ 

တစ်ခြား ဘယ် feature တွေကို remove လုပ်ပစ်လို့ရလဲဆိုတာမျိုးကိုလည်း correlation ကြည့်ပြီး ပြောလို့ရတယ်။ ပုံမှာ correlation matrix sample ပြထားပါတယ်။ 
sqft_living to sqft_living_15 သူတို့ရဲ့ correlation score ဆိုရင် တစ်ခြား nature မတူတဲ့ features တွေထက်စာရင် ပိုများတယ်။ 
တစ်ကယ်တမ်းကျတော့ sqft_living15 ဆိုတဲ့ feature သည် sqft_living ကနေ derive လုပ်လို့ရတယ်။ ဒီလိုနေရာမျိုးမှာ ဆိုရင် ပိုသင့်တော်တဲ့ တစ်ခုကိုပဲ သုံးလိုက်ရင် ရပြီ။

ကမ်းခြေမှာ shark attack လုပ်တဲ့ rate တိုးတယ်၊ တစ်ချိန်တည်းမှာ ice cream ရောင်းရတဲ့ rate လည်း တိုးလာတယ် ဆိုပါစို့။ ဒီနှစ်ခုက correlate မဖြစ်ဘူး။ ဒါပေမဲ့ 
ရာသီဥတု ပူလို့ shark attack rate တိုးတယ်၊ ပူလို့ လူတွေကမ်းခြေလာတာများကြလို့ ice cream ပိုရောင်းရတယ်။ cause က သွားတူနေတာမျိုး။ domain knowledge ကောင်းကောင်းရှိမှ
feature select လုပ်တဲ့ နေရာမှာ ပိုပြီး အဆင်ပြေမယ်။ 

ရှိပြီးသား features တွေကနေ အသစ်တွေထပ်ပြီး create လုပ်လို့ရတယ်။ ပိုပြီး သင့်တော်တဲ့ data လိုချင်တာ ဖြစ်ဖြစ် feature အရေအတွက် လျှော့ချချင်လို့ပဲ ဖြစ်ဖြစ် ဒီ strategy ကို သုံးလို့ရတယ်။
ရှိပြီးသွား data ကို aggregate လုပ်တာ, ဒါမှမဟုတ် ပိုပြီး အသေးစိတ်လိုချင်လို့ decompose လုပ်တာမျိုး။ ဥပမာ date ကနေ day, month, year ခွဲထုတ်တာ။

weight နဲ့ height အစား BMI ဆိုတာမျိုး formula တစ်ခုသုံးပြီး feature အသစ် create လုပ်လိုက်တာမျိုးလည်း လုပ်လို့ရတယ်။

ဒီမှာ ပြောခဲ့တဲ့ visualization, statistics values တွေ ထုတ်ကြည့်တာ, correlation, distribution ဒါတွေ အတွက် ကိုယ်တိုင် အစအဆုံး လုပ်စရာ မလိုဘူး။
python မှာဆိုရင် numpy, pandas, နောက် matplotlib စသည်ဖြင့် library တွေ သုံးပြီး ထုတ်ကြည့်လို့ရတယ်။

ဒီနေ့တော့ ဒီလောက်နဲ့ တော်လိုက်ပါဦးမယ်။ အချိန်ရရင် Data Warehousing နဲ့ Modeling အကြောင်း ဆက်ပြောပါဦးမယ်။