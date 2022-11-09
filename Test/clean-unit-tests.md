### Clean Tests

System တွေ develop လုပ်တဲ့ နေရာမှာ automated test တွေက ဘာလို့အရေးပါလဲဆိုတာ တော်တော်များများ
သိပြီးသား ဖြစ်ကြပါ။ TDD, BDD စတာတွေနဲ့ development လုပ်ပြီဆိုရင် test တွေကတော့ တစ်ချိန်လုံးနီးပါး ရေးနေရမှာပါ။
production code မှာ တစ်ခုခု ထပ်တိုးတာ ပြင်တာလုပ်မယ်ဆိုရင် သူနဲ့သက်ဆိုင်တဲ့ test တွေထပ်ထည့်တာ၊ ရှိပြီးသား test တွေကို 
ပြင်တာ စသည်ဖြင့် လုပ်ဖို့လိုတယ်။

ပထမဆုံး သိထားရမှာက test cases တွေက production level မှာ သုံးတဲ့ code တွေနည်းတူ clean ဖြစ်ဖို့လိုတယ်။ ဘာလို့လဲဆိုတော့ 
business logic တွေက အချိန်နဲ့အမျှ ပြောင်းနေမှာပဲ။ production code နဲ့အတူ test case တွေကလည်း လိုက်ပြီး evolve ဖြစ်နိုင်ဖို့လိုတယ်။

Test တွေကို clean ဖြစ်အောင် ဘယ်လို ရေးကြမလဲ။

#### Readability

Test တွေမှာ အရေးကြီးဆုံးက readability ပါ။ Test တစ်ခုကို ကိုယ်တိုင်ပဲဖြစ်ဖြစ်၊ တစ်ခြားသူပဲ ဖြစ်ဖြစ် လာဖတ်လိုက်တာနဲ့ 
ရိုးရှင်းနေဖို့လိုတယ်။ Test case ထဲမှာ သုံးထားတဲ့ expression တွေက ရှင်းလင်းပြီး ကျစ်လစ်နေရမယ်။ Expression တွေ နည်းလေကောင်းလေပဲ။

#### Small/One Concept per Test

Test တွေက small ဖြစ်ဖို့လိုတယ်။ assertions တွေ အများကြီးပါတာမကောင်းဘူး။ function တွေရေးရင် single purpose ဖြစ်အောင်
ရေးရသလိုပဲ test case တစ်ခုချင်းစီကလည်း ကြည့်လိုက်ရင် ဘာကို test လုပ်နေတာလဲဆိုတာ clear ဖြစ်ဖို့လိုတယ်။ 
Test case တစ်ခုမှာ assertion တစ်ခုတည်း သုံးဖို့ ဆိုတာမျိုးကတော့ လက်တွေ့မှာ မလွယ်ဘူး။ အဲ့တော့ best practice အနေနဲ့ test case တစ်ခုမှာ 
concept တစ်ခုစီ test လုပ်တာ အကောင်းဆုံးပဲ။


#### Use Meaningful Test Names

Test code ကို ဖတ်စရာမလိုပဲ test case name ကို ကြည့်လိုက်တာနဲ့ ဘာကို test လုပ်ချင်တာလဲဆိုတာ ဖော်ပြနေဖို့ လိုတယ်။ 
အတိုကောက်ရေးတာတွေ ရှောင်ရမယ်။ naming လုပ်တဲ့နေရာမှာ technical term တွေထက် ကိုယ့် software ရဲ့ domain နဲ့ဆိုင်တဲ့ terms တွေကို သုံးသင့်တယ်။

Testing လုပ်ဖို့ သုံးတဲ့ library တွေက API ကို တိုက်ရိုက်ခေါ်သုံးမဲ့အစား ကိုယ့်ရဲ့ domain နဲ့သက်ဆိုင်တဲ့ terms တွေကို သုံးပြီး
functions တွေ၊ test utilities တွေ ဆောက်ပြီးတော့ သူတို့ထဲမှာ ခုနက API တွေကို encapsulate လုပ်ပြီး သုံးသင့်တယ်။ 
တစ်နည်း ပြောရရင် domain specific testing language တစ်ခု ကိုယ်တိုင် ဆောက်တာမျိုးပေါ့။

#### Cover Edge Cases

Function တစ်ခုအတွက် test case တွေရေးပြီးဆိုရင် ဖြစ်နိုင်ချေရှိတဲ့ အခြေနေတွေ၊ edge cases တွေ အကုန်လုံးကို cover ဖြစ်အောင် test လုပ်ရမယ်။ 
correct input ပေးရင် correct output ရလားဆိုတဲ့ အခြေနေမျိုး ( Happy path လို့လည်း ခေါ်တယ် ) ကိုပဲ Test လုပ်တာမျိုးမကောင်းဘူးပေါ့။

#### Deterministic Tests

Test တွေက deterministic ဖြစ်ဖို့လိုတယ်။ Test လုပ်တဲ့ code ကို မပြင်သရွေ့ အဲ့ဒီ test ကို ဘယ်နှစ်ခါပဲ run ပါစေ same result ပဲရနေဖို့ အရေးကြီးတယ်။
မဟုတ်ရင် test case ကိုက reliable မဖြစ်တော့ ကိုယ်ရေးတဲ့ code ကိုဘယ်လိုသွားပြီး ကောင်းကောင်း အလုပ်လုပ်ပါတယ်လို့ verify လုပ်နိုင်မပါ့လဲ။ deterministic ဖြစ်ဖို့ဆိုရင် 
test cases တွေက independent ဖြစ်နေဖို့လိုတယ်။ တစ်ခြား test case တစ်ခုပေါ်ကို မှီခိုနေတာ၊ external state တစ်ခုခု အပေါ်မှီခိုနေတာမျိုး မဖြစ်သင့်ဘူး။

မေးစရာရှိတာက database call တို့ external API call တို့ပါရင်ရော ဘယ်လိုလုပ်မလဲပေါ့။ ဒီလိုနေရာမျိုးမှာ code level မှာ mock လုပ်ရင်လုပ်၊ 
မလုပ်ရင် API ဆိုလည်း mock server တစ်ခု spawn လုပ်၊ database ဆိုလည်း in memory instance လိုမျိုး spawn လုပ်လို့ရတယ်။ 
ကိုယ့်ရဲ့ codebase, architecture စတာတွေ နဲ့လည်း ဆိုင်တယ်။ ဥပမာ dependency injection မရှိဘူးဆိုပါစို့။ ကိုယ်က Class A ကို test လုပ်နေရင်း dependency တွေကို 
mock လုပ်ချင်တာမျိုးဆို တော်တော်ခက်ခဲမှာပါ။ implementation ကလည်း testable ဖြစ်ဖို့လိုသေးတာကို။ 

ကိုယ်က layered architecture သုံးတယ်ဆိုပါစို့။ Business Logic Layer က Persistence Layer (a.k.a. DB access) ပေါ်မှာမှိခိုနေတာမျိုးဆိုရင် Business Logic သီးသန့်
database မပါပဲ test လုပ်လို့မလွယ်ဘူး။ Hexagonal Architecture မှာဆိုရင် Business logic က တစ်ခြား layer တွေအပေါ် မမှီခိုပဲနဲ့ တစ်ခြား layer တွေက Business logic ပေါ်မှာ မှီခိုနေတာ။
dependency inversion လို့ခေါ်တယ်။ ဒီလိုနေရာမျိုးမှာ ဆိုရင် business logic ကို database or persistence layer မပါပဲ ကောင်းကောင်း test လုပ်လို့ရတယ်။

#### Arrange, Act, Assert

Test case တွေကို အများအားဖြင့် အပိုင်းသုံးပိုင်းခွဲလို့ရတယ်။ ပထမ တစ်ခုက test လုပ်ဖို့လိုတဲ့ data တွေ setup လုပ်တာ။ နောက်ပြီးရင် target function ပေါ်ကို test လုပ်မယ်။
နောက်ဆုံးအဆင့်အနေနဲ့ ရလာတဲ့ result မှန်မမှန် စစ်ဆေးတာ။ အနည်းဆုံး ဒီ step သုံးခုကို လိုက်နာသင့်တယ်။

နောက်ရှောင်ရမှာက တစ်ခုခုကို test လုပ်ဖို့ ကိုယ်ရေးထားတဲ့ implementation ကိုယ်ကိုပြန်သုံးတာမျိုး။ အောက်က example မှာကြည့်ရင်

```ts
// implementation
const sum = R.reduce(R.add, 0);

// test case
const numbers = [1, 2, 3];

const total = sum(numbers);
const expected = numbers.reduce(R.add)

expect(total).toEqual(expected)
```

implementation မှာလည်း number array ကိုပေါင်းဖို့ reduce ကိုသုံးထားတယ်။ test case ထဲမှာလည်း expected value နေရာမှာ ခုနက implementation ကိုပဲပြန်သုံးထားတယ်။
ဒီလိုမျိုး နေရာမှာတော့ ပြသနာက မသိသာပေမဲ့ တကယ့် လက်တွေ့မှာ business logic ကို implement လုပ်တဲ့ code ကိုယ်တိုင်ကမှားနေပြီဆိုရင် test case က အဲ့ဒီလို ပြသနာကို စစ်ထုတ်နိုင်မှာမဟုတ်ဘူး။

ကိုယ့် machine မှာပဲဖြစ်ဖြစ်၊ CI environment မှာပဲဖြစ်ဖြစ် test case တွေကို မြန်မြန်ဆန်ဆန် run လို့ရရမယ်။ ဒါမှ မကြာခဏ test တွေ run ဖြစ်မှာကိုး။ 
run ဖို့ကြာနေပြီဆိုရင် ရေရှည်မှာ test တွေမ run ပဲနဲ့ code ရေးဖို့ စဥ်းစားကြမှာပဲ။ မကောင်းဘူးပေါ့။

နောက်သတိထားရမှာ တစ်ခုက shared datasource (db, cache, etc.,) တွေကို testing အတွက်မသုံးဖို့ပါ။ test တွေကို parallel run တာမျိုး၊ test တစ်ခုကနေ test data တွေထည့်ပြီး clean up
လုပ်ဖို့ ကျန်ခဲ့တာမျိုးဆိုရင် race condition တွေရှိလာနိုင်တယ်။ အဲ့ဒီအခါကျရင် test တွေက randomly fail တာ randomly pass တာမျိုးတွေ ဖြစ်လာပါလိမ့်မယ်။ 
အဲ့တော့ database ကိုပါ ထည့်ပြီး test လုပ်ရမှာတွေပါခဲ့ရင် `test suite` တစ်ခုချင်းစီတိုင်းအတွက် in memory instance လိုမျိုး spawn လုပ်ပြီး သုံးသင့်တယ်။

Test code တွေကို မကြာခဏ refactor လုပ်ဖို့လိုပါတယ်။ ဒါမှရေရှည်မှာ automated test တွေကနေပေးတဲ့ benefits ကိုခံစားနိုင်မှာပါ။