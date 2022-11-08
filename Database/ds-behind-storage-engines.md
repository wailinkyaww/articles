### Data Structures behind Modern Database Storage Engines - Part 1

Databases တွေက သူတို့ကို  data တစ်ခုခုပေးရင် store  လုပ်ပေးမယ်၊ နောင်တစ်ချိန် လိုအပ်တဲ့အချိန်ကျရင် store ထားတဲ့ data ကို ပြန်ထုတ်ပေးမယ်။
အနိမ့်ဆုံး ဒီအလုပ်နှစ်ခုကို လုပ်ရတယ်။ အခု ဒီနေရာမှာ ပေးလိုက်တဲ့  data ကို ဘယ်လို  store လုပ်မလဲ၊ နောက်လိုအပ်လို့ querying  လုပ်တဲ့အခါ
ဘယ်လိုပြန်ပေးမလဲ ဒီနှစ်ခုကို database နေရာကနေ ကြည့်ကြည့်ပါမယ်။

[//]: # (TODO: transactional vs analytics)

Storage Engine တွေမှာ Log structured segmented storage engines (LSM) တွေနဲ့ Page oriented storage engines တွေရယ်ဆိုပြီး အဓိက type နှစ်မျိုး
အတွေ့များတယ်။ 

#### LSM Storage Engines

ပထမဆုံး text file ထဲမှာ key, value pairs တွေ line by line  append လုပ်ပြီး သိမ်းမယ်ဆိုပါစို့။ 
ပြန်ပြချင်ရင် သိမ်းထားတဲ့ line တွေထဲက key match ဖြစ်တဲ့ကောင်ကို for example: regex နဲ့တိုက်စစ်ပြီးပြန်ပြမယ်။

123: val1 </br>
456: val2 </br>
123: val3

ထပ်နေရင် ပိုပြီး recent ဖြစ်တဲ့ကောင်ကိုပြမယ်ဆိုပါစို့။ write အတွက်ကတော့ ရိုးရှင်းတယ် just append ဆိုတော့ performance အတွက် စိတ်ပူစရာမရှိဘူး။
read မှာက key နဲ့ရှာမယ်ဆိုရင် key match မဖြစ်မချင်း file တစ်ခုလုံးကို လိုက်ကြည့်နေရမှာ ဖြစ်တဲ့အတွက်  records တွေများလာလေလေ key တစ်ခုခုကို search လုပ်ဖို့ ဆိုးလာလေလေ ဖြစ်မှာပါ။
အဆိုးဆုံးအခြေနေမှာဆို complexity အရကြည့်ရင် O(n) ရှိလိမ့်မယ်။ ဆိုတော့ key တစ်ခုခုကို db ထဲမယ် ရှာတဲ့အချိန် efficient lookup ဖြစ်ဖို့ ပိုကောင်းတဲ့ solution တစ်ခုခုတော့ လိုပြီ။ 

Here, indexing comes in...

`Indexing` အတွက် သုံးတဲ့ data structures တွေကတော့ တစ်ခုထက်မက ရှိတယ်။ တစ်ခုချင်းဆီတိုင်းမှာ အနည်းနဲ့အများ trade off တွေတော့ ရှိကြတာပါပဲ။ 
ဒါပေမဲ့ ယေဘုယျ အနေနဲ့ ကြည့်ရင် indexing ဆိုတာက မူရင်း data ကနေ လိုအပ်တဲ့ structure အလိုက် metadata လေးတွေယူပြီး တစ်နေရာရာမှာ သိမ်းထားလိုက်တယ်။ additional data ပေါ့။
ကိုယ်က တစ်ခုခုရှာတော့မယ် query လုပ်တော့မယ်ဆိုရင် အဲ့ဒီ data သည် ဘယ်နေရာမှာ ရှိလဲဆိုတာ သိမ်းထားတဲ့ index ကနေ ပြပေးနိုင်တယ်။

နောက်တစ်ခုက index သည် မူရင်း data ကိုဘာမှ သွားမထိဘူး။ အပေါ်မှာပြောခဲ့ သလိုပဲ ရှိပြီးသား data ကနေ derived လုပ်တာ။ 
index ကိုသုံးလို့ write operation မှာတော့ performance တိုးစရာအကြောင်းမရှိဘူး။ 
data အသစ်ထပ်ထည့်တာ update လုပ်တဲ့အချိန်တွေမှာဆိုရင် index ကိုပါသွားပြီး update လုပ်ရမဲ့ step ပိုလာမယ်။ ဆိုတော့ write operation ကို slow down ဖြစ်သွားစေနိုင်ချေပဲရှိတယ်။
အဓိကကတော့ query ဆွဲတဲ့အချိန် performance ကောင်းအောင်ပဲ လုပ်ပေးနိုင်တယ်။ ဒါ့ကြောင့်မလို့ database အများစုက developer တွေကို application အလိုက် index လုပ်ချင်တဲ့ကောင်ကို 
manually ရွေးချယ်ခွင့်ပေးထားတာပါ။ developer အနေနဲ့ trade off  ကိုကြည့်ပြီး အကောင်းဆုံးဖြစ်မဲ့ကောင်ကို ရွေးရမဲ့ သဘောပါ။

#### Hash Indexes

Key, value data တွေကို hash indexes နဲ့ ဘယ်လို handle လုပ်မလဲကြည့်ကြည့်ရအောင်။ key,value pair တွေဆိုရင် programming languages တွေမှာရှိတဲ့ dictionary type လိုကောင်မျိုးနဲ့သိမ်းလို့ရတယ်။
အများစုကတော့ Hash map ( Hash Table ) နဲ့ implement လုပ်ကြတယ်။ Hash Map အကြောင်းကတော့ သိပြီးသားဖြစ်မှာပါ။ အရိုးရှင်းဆုံးပုံစံကို စဉ်းစားကြည့်ရင် file ထဲမှာ record တစ်ခုချင်းစီကို line by line သိမ်းတယ်ဆိုပါစို့။ 
ဘယ် key က memory offset ဘယ်လောက်မှာရှိတယ် ဆိုတာကို memory မှာ Hash Map အနေနဲ့ သိမ်းထားမယ်။ အသစ်တွေထပ်ဝင််လာတာဖြစ်ဖြစ် ဒါမှမဟုတ် ရှိပြီးသား key ရဲ့ value ကို update လုပ်တာပဲဖြစ်ဖြစ် 
memory မှာရှိတဲ့ Hash Map ကိုလည်း သွားပြီးတော့ update လုပ်မယ်။ db ထဲမှာ key တစ်ခုခုနဲ့ ရှာချင်တယ်ဆိုရင် Hash map ထဲမှာ အဲ့ဒီ key နဲ့သွားရှာလိုက်ရင် လိုချင်တဲ့ data ရဲ့ offset ကိုရမယ်ပေါ့။ 

ဒီလိုပုံစံသုံးထားတဲ့ database storage engine တွေ အပြင်မှာ တကယ်သုံးနေကြတာတွေရှိတယ်။ ဘယ်နေရာတွေမှာ ကောင်းလဲဆိုတော့ key ကတော့ တအား အများကြီးမရှိဘူး၊ ဒါပေမဲ့ key တစ်ခုတစ်ခုကို frequent update လုပ်တဲ့နေရာ ခဏခဏ update လုပ်
တဲ့အခြေနေမျိုးမှာ ဒီကောင်က တော်တော်လေး အဆင်ပြေတယ်။ ဘာလို့ဆို memory မှာ နေရာတွေ အများကြီး ယူစရာမလိုတာမလို့။

ခုနက data တွေကို actually သိမ်းတဲ့ပုံစံအကြောင်းကိုပြန်ပြောရရင် file ကို append လုပ်သွားတာက တစ်ချိန်ချိန်မှာ disk space ကုန်သွားနိုင်တယ်။ ဆိုတော့ ကောင်းတာက ကျွန်တော်တို့ သိမ်းချင်တဲ့ log တွေ record တွေကို file နဲ့သိမ်းမယ်၊ 
အဲ့ဒီ file ရဲ့ size က ပမာဏ တစ်ခုခုကို ရောက်လာရင် segment တစ်ခုအနေနဲ့ file တစ်ခုထားလိုက်မယ်။ နောက်ထပ်ဝင်လာတဲ့ writes တွေကို new segment ထဲမှာ သိမ်းမယ်။ segments တွေများလာပြီဆိုရင် အဲ့ဒီကောင်တွေကို merge လုပ်ပစ်လိုက်လို့ရတယ်။

ဥပမာ key,value နဲ့သိမ်းမယ်ဆိုရင် key တစ်ခုရဲ့ value ကို update လုပ်ချင်တယ်ဆိုရင် data ကိုသွားမပြင်ပဲ new record ကိုပဲ file ထဲမှာ append လုပ်လိုက်မယ်။ နောက်ပြန် query ဆွဲတဲ့ အချိန်ကျရင် most recent record ကိုပြန်ပြမှာဆိုတော့
key တူနေတဲ့ record တွေရှိနိုင်တယ်။ most recent write ကိုပဲပြန်ပြမှာဖြစ်တဲ့အတွက် old data တွေသည် အသုံးမဝင်ဘူး။ ဒီတော့ old data တွေကို ဖယ်ထုတ်ပစ်လိုက်လို့ရတယ်။ key တူတဲ့ record တွေသည် file တစ်ခုတည်းမှာ ရှိနိုင်သလို
မတူတဲ့ segments တွေမှာ တစ်နေရာစီရှိနေတာလည်းဖြစ်နိုင်တယ်။ file တွေကိုပြန်ပြီး merge လုပ်တဲ့အချိန်မှာ update မဖြစ်တော့တဲ့ data တွေကို ဖယ်လိုက်ရင် segment file size တွေရော့သွားမယ်။်
ဒီနေရာမှာ တစ်ခုမေးစရာရှိနိုင်တာက data ကို မပြင်ပဲ append only ပဲလုပ်နေတော့ record တစ်ခုခုကို ဖျက်ချင်ရင်ရောဘယ်လိုလုပ်မလဲဆိုတာပါ။ 

record တစ်ခုခုကိုဖျက်ချင်တယ်ဆိုရင် delete လုပ်မယ်ဆိုတဲ့ဆိုလိုရင်းနဲ့ special record တစ်ခု segment file ထဲကို append လုပ်လိုက်တယ်။ Tombstone လို့လည်းခေါ်တယ်။ segment file တွေ merge လုပ်တဲ့အချိန်ကျရင် delete လုပ်လိုက်တဲ့ key အတွက်
old data တွေကို merge ထဲမထည့်တော့ဘူး ဖယ်ပစ်လိုက်တဲ့သဘောပေါ့။ Tombstone က ချက်ချင်း delete မလုပ်သေးပဲ delete လုပ်ချင်တဲ့ကောင်အစား placeholder အနေနဲ့သုံးတဲ့ကောင်ပါ။ disk space ပိုထွက်လာမယ်ပေါ့။ compaction လုပ်
တယ်လို့ ခေါ်တယ်။ 

record တွေက တစ်ခါ write လုပ်ပြီးရင် update မရှိတော့ဘူးဖြစ်တဲ့အတွက် အရှေ့မှာ database က new read/write တွေကို handle လုပ်နေတဲ့အချိန်မှာ ခုနက merge လုပ်တာ compact လုပ်တာတွေကို background thread မှာ သွားလုပ်လို့ ရတယ်။ 
ထွက်လာတဲ့ result တွေကို new segment files တွေအနေနဲ့ write လုပ်လို့ရတယ်။ မူရင်း database ကိုဘာမှသွားထိမှာမဟုတ်ဘူး။ write လုပ်ပြီးတဲ့အချိန်ကျရင် database ကို old segment files တွေအစား file အသစ်တွေကို သုံးဖို့ပြောလိုက်ရင်ရပြီ။

ဘာပိုလာမလဲဆိုတော့ segment file တွေမှာ သူတို့နဲ့ သက်ဆိုင်တဲ့ Hash Table တွေ memory မှာအသီးသီးရှိမယ်။ key တစ်ခုခုရှာချင်တယ်ဆိုရင် recent အဖြစ်ဆုံး segment ရဲ့ hash map ကိုကြည့်မယ်။ 
အဲ့ထဲမှာမရှိရင် ဒုတိယ recent အဖြစ်ဆုံး segment ရဲ့ hash map စသည်ဖြင့် တစ်ဆင့်ချင်းစီ check သွားမယ်။ merge လုပ်ရင် segment file နည်းသွားမယ် တစ်ချိန်တည်းမှာ သက်ဆိုင်ရာ hash map အရေအတွက် လည်း လိုက်နည်းသွားမယ်။ 
အများကြီး လိုက် check လုပ်နေစရာမလိုတော့ဘူးပေါ့။

data သိမ်းတဲ့နေရာမှာ text file အနေနဲ့ပဲ အမြဲသိမ်းလို့တော့ efficient မဖြစ်ဘူး။ binary နဲ့သိမ်းတာပိုကောင်းတယ်။ Hash Map တွေကို in memory ထဲမှာသိမ်းထားတော့ database ကို အကြောင်းကြောင်းကြောင့် restart လုပ်မယ်ဆိုရင် ခုနက memory ပေါ်ကကောင်တွေ
lost ဖြစ်သွားမယ်။ restart ဖြစ်ကာမှ startup မှာ segment file တစ်ခုချင်းစီ scan ပြီး hash map ပြန်ဆောက် memory ပေါ်မှာပြန်သိမ်းအဲ့လိုတော့ လုပ်လို့ရတာပေါ့။ 
ဒါပေမဲ့လို့ segment file size ကကြီးနေရင် indexing ပြန်လုပ်နေရတာတင် အချိန်က တော်တော်ကြာနေလိမ့်မယ်။ တစ်ချို့ LSM သုံးတဲ့ engine တွေက segment တွေရဲ့သက်ဆိုင်ရာ Hash Map snapshot ကို disk ပေါ်မှာသွားသိမ်းထားလိုက်တယ်။ 
နောင်တစ်ချိန် လိုအပ်လို့ ပြန်ပြီး restart လုပ်ရင် ခုနက သိမ်းထားတဲ့ snapshot ကိုပဲပြန်ပြီးသုံးလိုက်ရုံပါ။ 

အပြင်ကနေ update လာရင် မူရင်းရှိနေတဲ့ကောင်ကို သွား update လုပ်တာမျိုးမဟုတ်ပဲ append only ပုံစံမျိုးနဲ့သွားတာက concurrency တို့ နောက် crash ဖြစ်သွားလို့ recovery လုပ်တဲ့နေရာမျိုးမှာ တစ်ခြား solution တွေထက်ပိုကောင်းတယ်။ နောက်တစ်ခုက
file ကို randomly write လုပ်တာထက်စာရင် writer thread ကို တစ်ခုပဲထားပြီး append only style နဲ့သွားတာသည် ဥပမာ SSD လိုကောင်မျိုးပေါ်မှာဆိုရင် ပိုပြီး efficient ဖြစ်တယ်။ 
data သည် immutable ဖြစ်မှာမလို့ multiple thread တွေကနေ concurrently read လုပ်လို့ရသွားမယ်။

ဒါက LSM engine တွေ အလုပ်လုပ်ပုံနဲ့ index အတွက် Hash Table သုံးတဲ့ ပုံစံကိုပြောပြတာပါ။ သူ့မှာလည်း trade off တွေတော့ရှိတယ်။ key တွေ အရမ်းများရင် hash map က memory ပေါ်မှာ ဆံ့မှာမဟုတ်တော့ဘူး။ 
disk ထဲသွားသိမ်းလို့ရပေမဲ့ ခဏခဏ I/O access လုပ်နေဖို့လိုလာမယ်။ performance အရမကောင်းဘူးပေါ့။ နောက်တစ်ခုက range queries တွေအတွက်လည်း efficient မဖြစ်ဘူး။

ကိုယ်ပိုင် database storage engine တစ်ခု build မလုပ်ဘူး ဆိုရင်တောင်မှ ကိုယ်လုပ်မယ့် software/project/application
အတွက် ဘယ် database က ပိုကောင်းတယ်၊ ဘယ်လို storage engine ကပိုပြီးအဆင်ပြေမယ် efficient ဖြစ်မယ်ဆိုတာကို
ရွေးချယ်တဲ့နေရာမှာ အထောက်အကူဖြစ််မှာပါ။
