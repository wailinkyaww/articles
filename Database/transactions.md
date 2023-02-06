Database Transactions

ဘာလို့ database transaction တွေ သုံးဖို့လိုလဲ၊ ဘယ်နေရာမှာ သုံးကြမလဲ၊ ဘယ်လိုတွေ အသုံးချလို့ရမလဲ စသည်ဖြင့်။
ကိုယ့်ရဲ့ system က reliable ဖြစ်ဖို့ဆိုရင် database နဲ့ပက်သက်ပြီးတော့ ထည့်စဥ်းစားစရာတွေ အများကြီး ရှိတယ်။

runtime မှာ database server down သွားတာမျိုး၊ application နဲ့ database ကြားက network connection shutdown ဖြစ်သွားတာမျိုး၊ 
ဒါမှမဟုတ် application server ကိုယ်တိုင်က crash ဖြစ်သွားမျိုး ဒီလိုမျိုးတွေ ဖြစ်နိုင်ခြေတွေရှိတယ်။ ဒါတွေက 
တစ်ချိန်လုံး ဖြစ်နေတာမျိုးတော့ မဟုတ်ဘူး။ client တွေအများကြီးကနေ data source တစ်ခုတည်းကို တစ်ချိန်တည်းမှာ ဝိုင်းပြီး update လုပ်ရင်လည်း race condition တွေရှိနိုင်တယ်။
database update တစ်ခုနဲ့ တစ်ခု overwrite ဖြစ်ပြီး data inconsistency တွေရှိလာနိုင်တယ်။

နောက်တစ်ခုက business logic တွေကို implement လုပ်တဲ့နေရာမှာ တစ်ချို့ data တွေက အတူတစ်ကွ ပြောင်းဖို့ update ဖြစ်ဖို့လိုတယ်။
ဥပမာ shopping cart application ဆိုပါစို့။ Product တစ်ခု အတွက် in stock item 5 ခုရှိမယ်။ တစ်ယောက်ယောက်က
အဲ့ဒီ Product နဲ့ item 3 ခုဝယ်လိုက်တယ်ဆိုပါစို့။ Order လို့ခေါ်မယ်ပေါ့။ user အတွက် order create လုပ်ပေးရမယ်။ 
တစ်ချိန်တည်းမှာ in stock ထဲကနေ ခုနက user ဝယ်လိုက်တဲ့ item count ကိုလည်း နှုတ်ဖို့လိုတယ်။ 
ဒီနေရာမှာ db operation နှစ်ခု ဆိုတော့ operation နှစ်ခုလုံး fail သွားရင်တော့ ပြသနာ မရှိဘူး၊ 
အဲ့လိုမဟုတ်ပဲနဲ့ တစ်ခုက success ဖြစ်ပြီး တစ်ခြားတစ်ခုက fail သွားတာမျိုးဆိုရင် data inconsistency တွေရှိလာမယ်။

ဒီလို ပြသနာတွေကို handle လုပ်ဖို့ transactions တွေကို သုံးတယ်။ transaction တွေကနေ ပေးနိုင်တဲ့ property တွေကို
ACID လို့ ခေါ်ကြတယ်၊ အသိများတယ်။

ACID - Atomicity, Consistency, Isolation, Durability

database တိုင်းကတော့ ACID မပေးဘူး။ တစ်ချို့ database တွေ (အများအားဖြင့် NoSQL database တွေ) က BASE လို့ခေါ်တဲ့ Basically Available, Soft State, and Eventual consistency ဒီ property တွေပဲပေးတယ်။ 
database တစ်ခုနဲ့ တစ်ခု ACID ကို implement လုပ်ပုံချင်းလည်း မတူကြဘူး။

Atomicity

Business operation တွေမှာ အများအားဖြင့် data source တစ်ခုထက် တစ်မျိုးထက်ပိုပြီး update လုပ်ရလေ့ရှိတယ်။ အပေါ်က ဥပမာမှာ ပြောခဲ့သလိုပဲ တစ်ချို့ data တွေက တစ်ချိန်တည်းမှာ 
အတူတစ်ကွ ပြောင်းဖို့ update ဖြစ်ဖို့လိုတယ်။ unit တစ်ခုပေါ့။  ဥပမာ database write နှစ်ခုရှိတယ် ဆိုပါစို့။ 

txn starts
 - create an order
 - update `in stock` item count  
txn ends

Atomic ဖြစ်တယ်ဆိုတာက ဒီ business operation တစ်ခုလုံး success ဖြစ်ရင်ဖြစ်၊ မဖြစ်ရင် operation တစ်ခုလုံး fail ဖြစ်သွားတာမျိုးကို ခေါ်တယ်။ 
တစ်ချို့ တစ်ဝက်ကပဲ success ဖြစ်တာမျိုး ဖြစ်လို့မရဘူး။ အဲ့တော့ ဘယ်လိုအခြေနေမှာ မဆို success ဖြစ်ရင်ဖြစ်၊ မဖြစ်ရင် တစ်ခုခု fail သွားတာနဲ့ transaction ကို abort လုပ်လို့ရရမယ်။
write လုပ်ပြီးသွားတဲ့ db operation တွေကို undo လုပ်တာပေါ့။ manually လုပ်မယ့် အစား database ကနေ လုပ်ပေးနိုင်ရမယ်။ ဒီ property ကိုပေးနိုင်ရင် atomic ဖြစ်တယ်လို့ ပြောလို့ရတယ်။

data ကို update လုပ်တယ်လို့ပြောတဲ့ နေရာမှာ database ထဲက data တွေကိုပဲဆိုလိုတာ မဟုတ်ဘူး။  business logic တွေကို handle လုပ်တဲ့နေရာမှာ 
ကိုယ်က ဘယ်ကောင် ကို အရင်လုပ်လဲ နောက်မှ လုပ်လဲဆိုတဲ့ order ကလည်း အရေးကြီးတယ်။ ဆိုပါစို့ database ထဲမှာ တစ်ခုခု update လုပ်ချင်တယ်။ တစ်ခြား 3rd party API တစ်ခုကိုလည်း update request တစ်ခုလုပ်မယ်။

txn starts
 - update username in db
 - call 3rd API (e.g., Twilio Chat) to update username
txn ends

အပေါ်က order အရ db က atomic ဖြစ်တယ်ဆိုရင် API call fail ရင် db write ကို rollback လုပ်လို့ရတယ်။ ဘာလို့လဲဆို db write ကအရင် လာလို့။ အောက်က ဥပမာ ကို တစ်ချက်ကြည့်ရအောင်။

txn starts
 - call 3rd API (e.g., Twilio Chat) to update username
 - update username in db
txn ends

ပြသနာက ဒီလိုနေရာမျိုးမှာ ကိုယ်က API call ကို အရင်ခေါ်လိုက်လို့ သူကတော့ success ဖြစ်သွားတယ်။ 
နောက်မှလာတဲ့ db write က fail ရင် အရင်လုပ်ပြီးသွားတဲ့ API call ကို revert လုပ်ဖို့ ပိုခက်ခဲသွားပြီ။ တစ်ချို့နေရာမျိုးမှာဆို မဖြစ်နိုင်ဘူးပေါ့။ 
ဒီတော့ order အစီအစဥ် ကလည်း အရေးကြီးပါတယ်။ တစ်ချို့ အရာတွေက database ကနေပဲ လုပ်ပေးလို့ မရဘူး ဆိုတာကို ပြောချင်တာပါ။

တစ်ချို့အခြေနေမှာ api call ကို အရင်ခေါ်ပြီးမှ ရလာတဲ့ result ကို db ထဲမှာ update ရတာမျိုးတွေလည်းရှိတယ်။ ဒီလို အခြေနေတွေမှာ db update fail သွားရင် recover လုပ်ဖို့အတွက်
အပေါ်မှာပြောခဲ့တဲ့ eventual consistency လိုကောင်မျိုးသုံးကြတယ်။ ဒါကတော့ atomicity နဲ့မဆိုင်လို့ ထည့်မပြောတော့ပါဘူး။ ရှာဖတ်ကြည့်ပါ။

Isolation

database တွေက အများအားဖြင့် client တွေအများကြီးကို serve လုပ်ရတယ်။ ဥပမာ application ကို horizontal scaling လုပ်လို့ same database ကို
application instance တွေ အများကြီးကနေ တစ်ပြိုင်တည်း သုံးနေတာမျိုးဖြစ်ဖြစ်၊ ဒါမှမဟုတ် application server instance တစ်ခုတည်း ရှိရင်တောင် request တွေအများကြီးကို server က တစ်ချိန်တည်းမှာ 
handle လုပ်နေတာမျိုးဆိုရင် database ကိုလည်း concurrent access (read, write) လုပ်ရတာတွေ ရှိလာမယ်။ မတူတဲ့ data တွေကို access လုပ်နေတာဆိုရင်တော့ ပြသနာမရှိဘူး။

database record တစ်ခုတည်းကို multiple client တွေကနေ modify လုပ်နေပြီဆိုရင်တော့ concurrency issue တွေရှိလာမယ်။ race condition တွေပေါ့။
ဥပမာ finance application တစ်ခု ဆိုပါစို့။ user ရဲ့ wallet ထဲမှာ 10,000 ရှိတယ်။ wallet deduct transaction နှစ်ခု တစ်ပြိုင်တည်း နီးပါး execute လုပ်ချင်တယ်။ 
wallet ကိုအရင် read လုပ်မယ် ပြီးရင် deduct amount ကို နှုတ်ပြီးရလာတဲ့ amount ကို update လုပ်မယ် ဆိုကြပါစို့။ ဒီနေရာမှာ read လုပ်တဲ့ အချိန်နဲ့ ပြန်ပြီး write (update) လုပ်တဲ့အချိန်ကြားမှာ delay ရှိတယ်။

Wallet balance : 10,000
First deduct : 5,000
Second deduct : 3,000

first request က wallet balance ကို read လုပ်တဲ့အချိန် 10,000 ရမယ်။ ဒီ request ကနေ deduct လုပ်ပြီး ရလာတဲ့ amount ပြန်ပြီး update မလုပ်ရသေးခင် 
တစ်ခြား second deduct request ကို execute လုပ်လို့ wallet balance ကို read လုပ်မယ်ဆိုရင် 10,000 ပဲရနေဦးမယ်။
ဒီအခြေနေမှာဆိုရင် second request ရဲ့ update က နောက်မှပြီးတယ်ဆိုရင် final amount က 7,000 လို့ရမယ်။
first request ရဲ့ update က နောက်မှပြီးဆိုရင် final amount က 5000 ဖြစ်နေမယ်။ deduct tranx နှစ်ကြောင်း ကနေဖြတ်လိုက်လို့ ရရမယ့် correct amount - 2000 က race condition သာရှိခဲ့ရင် ဘယ်လိုမှ မရနိုင်ဘူး။

database တစ်ခုက isolation ပေးနိုင်တယ်ဆိုရင် developer အနေနဲ့ တစ်ချိန်မှာ database တစ်ခုလုံးမှာ transaction တစ်ခုပဲ run နေတယ်လို့ ယူဆပြီးတော့ handle လုပ်လို့ရတယ်။
database ကနေ transaction တွေကို isolate လုပ်ပေးထားတာ။ တစ်ခုနဲ့ တစ်ခုမမြင်ရဘူးပေါ့။ isolation လုပ်တဲ့နေရာမှာလည်း ဘယ်လောက် အတိုင်းအတာ အထိ စိတ်ချရလဲ safe ဖြစ်လဲဆိုတဲ့ isolation level တွေရှိတယ်။

Isolation Levels

Read uncommitted - ဒီကောင်က မတင်းကျပ်ဆုံး isolation level လို့ပြောလို့ရတယ်။ တစ်ခြား transaction တွေကနေ write လုပ်ထားတယ် ဒါပေမဲ့ commit မလုပ်ရသေးတဲ့ data တွေကို read လုပ်လို့ရတယ်။
dirty read လို့ခေါ်တယ်။ ဘာလို့လဲဆိုရင် commit မလုပ်ရသေးတာမလို့ ပြန်ပြီး rollback ဖြစ်သွားနိုင်ချေရှိလို့။ ဒီကောင်ကို ရှောင်တာတော့ အကောင်းဆုံးပါပဲ။ ဒါပေမဲ့လို့ ကိုယ်က ACD တော့လိုချင်တယ်၊ တစ်ချိန်တည်းမှာ high concurrency လိုချင်လို့
isolation ကို သိပ်ပြီး ဂရုမစိုက်ဘူးဆိုတဲ့ အခြေနေမျိုးမှာဆိုရင်တော့ အသုံးဝင်ပါတယ်။

Serializable ကတော့ strict အဖြစ်ဆုံး isolation level ပါ။ တစ်ဖက်မှာ transaction တစ်ခုနဲ့ တစ်ခုကြား isolate ဖြစ်ပါတယ်လို့ အပြည့်အဝ နီးပါး အာမခံ ပေးနိုင်တယ်။ ဒါပေမဲ့ တစ်ဖက်မှာ application ရဲ့ performance ကိုသွားပြီး ထိခိုက်တယ်ပေါ့။
လုံးဝကို အမှားခံလို့ မရတဲ့ data ကို handle လုပ်ရတဲ့ အခါမျိုးမှာ သုံးကြတယ်။

ဒီနှစ်ခုကြားမှာ read committed နဲ့ repeatable read ဆိုတဲ့ တစ်ခြား isolation level နှစ်ခု ရှိသေးတယ်။ application ရဲ့လိုအပ်ချက် ပေါ်မူတည်ပြီးတော့ ကိုယ်နဲ့ ကိုက်ညီမဲ့ ကောင်ကို ရွေးရမှာပါ။
နောက် သတိထားရမှာ တစ်ခုက ကိုယ်သုံးနေတဲ့ database သည် isolation level ကို ဘယ်လို implement လုပ်ထားလဲဆိုတာမျိုးပါ။ 
ဥပမာ Oracle db ရဲ့ serializable level ဆိုရင် သူက နောက်ကွယ်မှာ snapshot isolation ကိုသုံးတယ််။ serializable အစစ်မဟုတ်ဘူးပေါ့။ အပြည့်အဝ စိတ်မချရဘူးပေါ့။

Consistency

သူကတော့ database ထဲရှိတဲ့ data တွေ မှန်မမှန်၊ သတ်မှတ်ထားတဲ့ constraints တွေနဲ့ ကိုက်ရဲ့လား ဆိုတာမျိုးကို enforce လုပ်ပေးနိုင်တဲ့ property ပေါ့။ 
data တွေ consistent ဖြစ်ရဲ့လားပေါ့။ data တွေ consistent ဖြစ်ရဲ့လားဆိုတဲ့နေရာမှာ သိမ်းတဲ့ data တွေရဲ့ data type တို့၊ တစ်ခုနဲ့ တစ်ခုကြား relationship တွေ၊
foreign key constraints တွေ၊ နောက် uniqueness လိုမျိုး စတာမျိုးတွေကိုတော့ database ကနေ schema လိုကောင်မျိုးနဲ့ ထိန်းပေးလို့ရတယ်။ ဒါပေမဲ့လို့
အပေါ်က example လိုမျိုး deduct transaction နှစ်ကြောင်း run လို့ ရတဲ့ data သည်မှန်ရမယ် ဆိုတာမျိုးကိုတော့ database က အလိုအလျောက်မလုပ်ပေးနိုင်ဘူး။ ဒါကတော့ developer ရဲ့တာဝန်ပါ။

Durability

ဒီတစ်ခုကတော့ database တစ်ခုမှာ transaction တစ်ခု commit ဖြစ်သွားပြီရင် data က persist ဖြစ်သွားပြီဆိုတာကို အာမခံချက်ပေးနိုင်တာမျိုးပါ။ 
transaction commit လုပ်ပြီးသွားတဲ့ အချိန် အကြောင်း တစ်ခုခုကြောင့် database server down သွားတာမျိုးဆိုရင်တောင် data ကျန်နေဦးမယ်လို့ ဆိုလိုချင်တာပါ။
db ထဲကို write မလုပ်ခင် ကြိုပြီး log ရိုက်ထားတာမျိုး၊ တစ်ခြား storage တွေမှာ replicate လုပ်ပြီး backup ထားတာမျိုး စတာမျိုးတွေ သုံးပြီး durability ပေးနိုင်အောင် လုပ်ကြတယ်။

ကိုယ့် software ရဲ့ infrastructure နဲ့ architecture ပေါ်မူတည်ပြီး database ကနေပေးတဲ့ ACID နဲ့တင်
Business Logic ကို ကောင်းကောင်း handle လုပ်လို့ ရမရ ဆိုတာမျိုးတွေလည်း ရှိတယ်။ microservice services တွေမှာ service အလိုက် separate database တွေသုံးထားတယ် ဆိုပါစို့။
အပေါ်က shopping cart example မှာပဲ ပြန်ကြည့်ရင် product service တစ်ခု၊ order service တစ်ခု ရှိမယ်ဆိုရင်
order create လုပ်ရင် product service က in stock item count ကိုပါသွားပြီး update လုပ်ရမှာ ဖြစ်တဲ့ အတွက် normal transaction တွေနဲ့တင် မလုံလောက်ဘူး။

multi database ဖြစ်နေလို့။ 2PC လို့ခေါ်တဲ့ 2 Phase Commit လိုကောင်မျိုးသုံးလို့ရတယ်။ ဒါပေမဲ့လို့ ဒီနေရာမှာဆို microservice ရဲ့ အရေးကြီးတဲ့ property တစ်ခုဖြစ်တဲ့ availability ကိုသွားပြီး ထိခိုက်မယ်။ 
ဘာလို့လဲဆိုရင် 2PC က synchronous communication ပုံစံတစ်ခုဖြစ်နေလို့။ Order service သည် Product service ကို မှီခိုနေတဲ့ သဘောမျိုးပဲ။ 
ဒီလိုနေရာမှာ ဆိုရင် 2PC မဟုတ်တဲ့ တစ်ခြား technique တွေကိုသုံးပြီး data consistency ကိုထိန်းရတယ်။

database transaction တွေ အကြောင်း အတိုင်းအတာ တစ်ခုအထိတော့ သိသွားမယ်ထင်ပါတယ်။ ကျန်တာတော့ ကိုယ်တိုင် ရှာဖတ်ကြည့်ပါ။