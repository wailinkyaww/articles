Database Transactions

ဘာလို့ database transaction တွေ သုံးဖို့လိုလဲ၊ ဘယ်နေရာမှာ သုံးကြမလဲ၊ ဘယ်လိုတွေ အသုံးချလို့ရမလဲ စသည်ဖြင့်။
ကိုယ့်ရဲ့ system က reliable ဖြစ်ဖို့ဆိုရင် database နဲ့ပက်သက်ပြီးတော့ ထည့်စဥ်းစားစရာတွေ အများကြီး ရှိတယ်။

software runtime မှာ database server down သွားတာမျိုး၊ application နဲ့ database ကြားက network connection shutdown ဖြစ်သွားတာမျိုး၊ 
ဒါမှမဟုတ် application server ကိုယ်တိုင်ကိုက crash ဖြစ်သွားမျိုး ဒီလိုမျိုးတွေ ဖြစ်နိုင်ခြေတွေရှိတယ်။ ဒီဟာတွေက
တစ်ချိန်လုံး ဖြစ်နေတာမျိုးတော့ မဟုတ်ဘူး။ client တွေအများကြီးကနေ data source တစ်ခုတည်းကို တစ်ချိန်တည်းမှာ ဝိုင်းပြီး update လုပ်ရင်လည်း race condition တွေရှိလာနိုင်တယ်။
database update တစ်ခုနဲ့ တစ်ခု overwrite ဖြစ်ပြီး data inconsistency တွေရှိလာနိုင်တယ်။

နောက်တစ်ခုက business logic တွေကို implement လုပ်တဲ့နေရာမှာ တစ်ချို့ data တွေက အတူတစ်ကွ ပြောင်းဖို့ update ဖြစ်ဖို့လိုတယ်။
ဥပမာ shopping cart application မှာ Product တစ်ခု အတွက် in stock item 5 ခုရှိမယ်။ တစ်ယောက်ယောက်က
အဲ့ဒီ Product နဲ့ item 3 ခုဝယ်လိုက်တယ်ဆိုပါစို့။ Order လို့ခေါ်မယ်ပေါ့။ ဒီ user ရဲ့ order ကို create လုပ်ရမယ်။ 
တစ်ချိန်တည်းမှာ ခုနက in stock ထဲက item count ကိုလည်း update ဖို့လိုတယ်။ ဒီနေရာမှာ db operation နှစ်ခု ဆိုတော့ operation နှစ်ခုလုံး fail သွားရင်တော့ ပြသနာ မရှိဘူး၊ 
အဲ့လိုမဟုတ်ပဲနဲ့ တစ်ခုက success ဖြစ်ပြီး တစ်ခြားတစ်ခုက fail သွားတာမျိုးဆိုရင် data inconsistency တွေရှိလာမယ်။

ဒီလို ပြသနာတွေကို handle လုပ်ဖို့ transactions တွေကို သုံးတယ်။ transaction တွေကနေ ပေးနိုင်တဲ့ property တွေကို
ACID လို့ အသိများတယ်။

ACID - Atomicity, Consistency, Isolation, Durability

database တိုင်းကတော့ ACID မပေးဘူး။ database တစ်ခုနဲ့ တစ်ခု ACID ကို implement လုပ်ပုံချင်းလည်း မတူကြဘူး။ 
ကိုယ့် software ရဲ့ infrastructure နဲ့ architecture ပေါ်မူတည်ပြီး database ကနေပေးတဲ့ ACID နဲ့တင် Business Logic ကို ကောင်းကောင်း handle
လုပ်လို့ ရမရ ဆိုတာမျိုးတွေလည်း ရှိတယ်။ ကိုယ်က microservice architecture နဲ့ service တစ်ခုချင်းစီကို separate database တစ်ခုစီ သုံးပြီးသွားနေတယ် ဆိုပါစို့။ 
ခုနက shopping cart example မှာပဲ ပြန်ကြည့်ရင် product service တစ်ခု၊ order service တစ်ခု ရှိမယ်ဆိုရင်
order create လုပ်ရင် product service က in stock item count ကိုပါသွားပြီး update လုပ်ရမှာ ဖြစ်တဲ့ အတွက် normal transaction တွေနဲ့တင် မလုံလောက်ဘူး။

multi database ဖြစ်နေလို့။ 2PC လို့ခေါ်တဲ့ 2 Phase Commit လိုကောင်မျိုးသုံးလို့ရတယ်။ ဒါပေမဲ့လို့ ဒီနေရာမှာဆို microservice ရဲ့ အရေးကြီးတဲ့ property တစ်ခုဖြစ်တဲ့
availability ကိုသွားပြီး ထိခိုက်မှာပေါ့။ ဘာလို့လဲဆိုရင် 2PC က synchronous communication ပုံစံတစ်ခုဖြစ်နေလို့။ 
Order service သည် Product service ကို မှီခိုနေတဲ့ သဘောမျိုးပဲ။ ဒီလိုနေရာမှာ ဆိုရင် 2PC မဟုတ်တဲ့ တစ်ခြား technique တွေကိုသုံးပြီး data consistency ကိုထိန်းရတယ်။ 