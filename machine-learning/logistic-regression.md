### Logistic Regression

ပုံမှန် linearity ကို ခန့်မှန်းဖို့ Traditional Linear Regression model တွေ သုံးကြတယ်။ တစ်ဆင့်ပိုပြီး

- binary values (yes/no)
- counts
- categorical (eg., Grade A/B/C)

ဒီလို response တွေကို modeling လုပ်ချင်တယ် ဆိုရင် simple linear regression လောက်နဲ့မရတော့ဘူး။
Generalized Linear Models တွေကို သုံးရတယ်။ GLMs တွေမှာ ဆိုရင် ပုံမှန် Linear Regression model တွေပါမယ်။
binary outcomes တွေ အတွက်ဆိုရင် Logistic Regression, နောက် counting အတွက်ဆိုရင် Poisson Regression တို့ သုံးလို့ရတယ်။

Predictor feature တစ်ခု ဒါမှမဟုတ် တစ်ခုထက်ပိုရှိမယ်။
Response သည် binary values တွေလိုချင်တယ်။ ခန့်မှန်းခြေ Probability ဘယ်လောက်ရှိမလဲ သိချင်တယ်။
ဒီလို အခြေနေမျိုးမှာ Logistic Regression ကို သုံးလို့ရတယ်။

#### Linear Combination

ပထမဆုံး ကျွန်တော်တို့ရဲ့ features တွေကနေ linear combination တစ်ခုရှိမယ်။

z = β0 + β1 . X1 + β2 . X2 + .... + βk . Xk

ဒီမှာ ကျွန်တော်တို့ရဲ့ z သည် -∞ ကနေ +∞ အထိ ကြားထဲက value တစ်ခုခု ဖြစ်နိုင်တယ်။

Logistic Regression ကို abstract လုပ်လိုက်ရင် features တွေနဲ့ သက်ဆိုင်ရာ weights/coef တွေရှိမယ်။
အခု ရလာတဲ့ Linear Combination ကို သုံးပြီးတော့ output probability ကို predict လုပ်ချင်တယ်။
ဒီတော့ probability ကို ဘယ်လိုရှာကြမလဲ။

value အရကြည့်မယ် ဆိုရင် probability values တွေသည် 0 ကနေ 1 အတွင်းပဲ ဖြစ်နိုင်တယ်။
ကျွန်တော်တို့ရဲ့ linear combination (z) value က အပေါ်မှာ ပြောခဲ့တဲ့ အတိုင်း -∞ ကနေ +∞ အတွင်း ရှိမယ်။

သေချာတာတော့ ကျွန်တော်တို့ z = p ဆိုပြီး equate လုပ်လိုက်လို့ အဆင်မပြေဘူး။

#### Odds

event တစ်ခုရဲ့ ဖြစ်နိုင်ခြေနဲ့ မဖြစ်နိုင်ခြေ ယှဥ်ကြည့်လိုက်ရင် ratio ဘယ်လောက်ရှိမလဲ ဆိုတာကို odds လို့ခေါ်တယ်။
mathematically အရဆိုရင်

odds = p/(1-p)

ဒီနေရာမှာ p က event တစ်ခုရဲ့ ဖြစ်နိုင်ခြေ probability။
ဥပမာ p က 0.75 ဆိုရင်

odds = 0.75/0.25 = 3

event ရဲ့ ဖြစ်နိုင်ခြေသည် မဖြစ်နိုင်ခြေထက် သုံးဆပိုများတယ် လို့ပြောလို့ရတယ်။

p က 0 ဆိုရင် odds သည် 0။
p က 1, event က အမြဲ ဖြစ်နေမယ် ဆိုရင် odds သည် +infinity နဲ့ ပိုပိုပြီး နီးလာမယ်။

odds -> 0 to +infinity
linear combination -> -infinity to +infinity

z = odds ဆိုပြီး equate လုပ်လိုက်လို့ မရသေးဘူး။
linear combination နဲ့ odds ရဲ့ range ယှဥ်ကြည့်ရင် ကွဲနေတာ တွေ့ပါလိမ့်မယ်။
mapping လုပ်လို့ အဆင်မပြေသေးဘူး။

predictor တွေမှာ unit တစ်ခု increase လုပ်လိုက်ရင် output ( ဒီနေရာမှာဆို probability ) မှာ ဘယ်လောက်သွားပြီး effect
ဖြစ်နိုင်လဲဆိုတဲ့ အချက်ကို interpretability လို့ခေါ်တယ်။ ဒီ equation နဲ့ဆိုရင် interpret လုပ်လို့ မလွယ်ဘူး။

#### Log-Odds

Log ကတော့ ဘာကို ပြောတယ် ဆိုတာ သိကြမှာပါ။ log-odds သည် ခုနက ကျွန်တော်တို့ အပေါ်မှာ ရလာတဲ့ odds ရဲ့ natural logarithm ပဲ။

log-odds = ln (p/(1-p))

ln ကို 0 နဲ့ close ဖြစ်တဲ့ small number တွေပေးလိုက်ရင် သူက -∞ နဲ့ ပိုနီးတဲ့ values တွေပြန်ပေးလိမ့်မယ်။
အလားတူ အရမ်းကြီးတဲ့ number တွေပေးမယ် ဆိုရင် +∞ ဖက်ကို mapping လုပ်ပေးမယ်။

တစ်နည်းပြောရရင် ကျွန်တော်တို့ရဲ့ log-odds function က p (range 0 to 1) တစ်ခုခုပေးလိုက်ရင် -∞ to +∞ အတွင်း map
လုပ်ပေးနိုင်တယ်။
ကျွန်တော်တို့က linear combination ပေးပြီးတော့ p value လိုချင်တာ။ inverse ပေါ့။

z = ln(p/(1-p)) လို့ equate လုပ်လိုက်မယ်။ ကျွန်တော်တို့ လိုချင်တာက probability။ current equation ကို inverse
လုပ်လိုက်ရင်
လိုချင်တဲ့ p ရပြီ။

p = 1 / (1+e^(-z))
σ(z) = 1 / (1+e^(-z))

logistic function (sigmoid of z) လို့လည်းခေါ်ကြတယ်။

GLM term တွေအရဆိုရင် log-odds ကို link function လို့ခေါ်လို့ရတယ်။
linear combination နဲ့ ကျွန်တော်တို့လိုချင်တဲ့ value နှစ်ခုကြားမှာ link လုပ်ပေးတဲ့ ကောင်မလို့။

Training လုပ်တဲ့ အချိန်မှာ ကျွန်တော်တို့မှာ linear combination (z) လည်းရှိတယ်။ သူတို့နဲ့ သက်ဆိုင်တဲ့ label 0/1
လည်းရှိပြီဆိုတော့ probability value အနေနဲ့ သုံးပြီး train လုပ်လို့ရတယ်။

ဒီကနေမှ linear equation အတွက် သက်ဆိုင်ရာ weights/coef တွေရှာလိုက်မယ်။
β0, β1, β2, ..., βk အထိ ရပြီဆိုရင် predict လုပ်တဲ့ နေရာမှာ ပြန်သုံးလို့ရပြီ။

Training လုပ်တဲ့ process မှာ weights/coef တွေရှာဖို့ အတွက် Maximum Likelihood Estimation လို algorithm တွေ သုံးကြတယ်။

sigmoid ရဲ့ curve သည် S ပုံစံရှိတယ်။ ပုံမှာ sample ပြထားပါတယ်။

features တွေ အများကြီးရင် သူတို့ကြားမှာ multicollinearity ရှိနိုင်လို့ regularization technique တွေ သုံးရတယ်။
multicollinearity ဆိုတာက feature တစ်ခုနဲ့ တစ်ခု အရမ်းကို correlate ဖြစ်နေတာ။
feature တစ်ခုကို တစ်ခြား features တွေကနေ ပြန်ပြီး predict လုပ်လို့ရနေတာမျိုးကို ခေါ်တာပါ။

mathematical အတော်လေး ဆန်ကောင်းဆန်နေနိုင်တယ်။ ဒါပေမဲ့ logistic function ကို ဒီတိုင်း formula ကြည့်ပြီး
သုံးလိုက်တာထက်စာရင်
ဘယ်ကနေ လာတယ် ဘာလို့ ဒီကောင်ကို သုံးရတယ် ဆိုတဲ့ sense ရသွားအောင်လို့ပါ။