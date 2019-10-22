# Densaku App တွင် Google Analytics(GA) နှင့် Google Tag Manager(GTM) ကိုအသုံးပြုခြင်း

## ကိုးကားစာများ
https://www.orbitmedia.com/blog/what-is-google-tag-manager-and-why-use-it/

## Use Case Scenario
- Top Page View Count, Product List Page View Count နှင့် Product View Count တို့ကို code အတတ်နိုင်ဆုံးနည်းအောင်ရေး၍ လုပ်ရန်

## သီအိုရီတွေးတောခြင်း
- Q: Google Analytics(GA) ဘာလဲ? ဘယ်လဲ? <br>
 A: GA ဆိုတာက website တွေရဲ့ အခြေအနေအမျိုးမျိုးကို လေ့လာစောင့်ကြည့်တဲ့ ဝန်ဆောင်မှုဖြစ်ပါတယ်။
- Q: Google Tag Manager(GTM) ဘာလဲ? ဘယ်လဲ? <br>
 A: GTM ဆိုတာက website တွေရဲ့ event အမျိုးမျိုး (button click, link click, page load) ကို page source code မှာ သွားရေးနေစရာမလိုဘဲ track လုပ်ပေးတဲ့ ဝန်ဆောင်မှုဖြစ်ပါတယ်။ သူက event တွေ fire ဖြစ်တိုင်း Third party service တွေကို event information data တွေပို့ပေးမဲ့ code လို့ပြောလည်းရပါတယ်။ 
- Q: Page view count ကြည့်ဖို့ဆို GA တစ်ခုတည်းနဲ့ မလုံလောက်ဘူးလား? <br>
 A: လုံလောက်ပါတယ်။ ဒါပေမဲ့ Product view count အတွက်ကြတော့ product code နဲ့ product name ပါတွဲပြချင်တဲ့အတွက် website ကနေ customized data တွေပို့နိုင်ဖို့ရာ GTM ကိုသုံးရပါတယ်။

## GA စတင်သုံးစွဲခြင်း
1. analytics.google.com သို့သွားပါ။
2. login မဝင်ရသေးရင် login ဝင်ပါ။
3. create account နှိပ်လိုက်ပါ။ 
4. account name ထည့်ပါ။ ကျန်တာဒီတိုင်းထားပြီး Next နှိပ်ပါ။<br>
 <img src="images/ga-setup-1.png">
5. Web ကိုပဲထားပြီး Next နှိပ်ပါ။
 <img src="images/ga-setup-2.png">
6. Property Setup ရောက်ပါပြီ။
 - Website Name: ကိုကြိုက်တာပေးပါ။
 - Website URL: den-saku url ထည့်ပါ။ local ဆို 127.0.0.1 ဆိုပြီးပဲထည့်ပါ။
 - Industry Category: Shopping ပဲရွေးလိုက်ပါ။
 - Reporting Time Zone: real site အတွက် Japan ရွေးပါ။ local ဆို Myanmar time ပဲရွေးလိုက်ပါ။
 - Create နှိပ်ပါ။
 <img src="images/ga-setup-3.png">
 
7. Term of Service တွေ၊ User Agreement တွေကို Accpet လုပ်ပြီး အောက်ဆုံးက I Accept button ကိုနှိပ်ပါ။
8. အောက်ပုံကျလာပါမယ်။ GA account တစ်ခုနဲ့ Property တစ်ခုတည်ဆောက်လို့ပြီးပါပြီ။ Tracking ID ကို Copy ကူးပြီး notepad ပေါ်ခဏတင်ထားလိုက်ပါ။
 <img src="images/ga-setup-4.png">
9. အပေါ်အစိမ်းရောင်အဝိုင်းကို select လုပ်ပြီး ကျွန်တော်တို့ GA အကောင့်တွေ Property တွေကို ပြောင်းကြည့်လို့ရပါတယ်။
10. Google အကောင့်တစ်ခုအတွက် GA အကောင့် ၁၀ ခုရပါတယ်။ GA အကောင့် ၁ခုမှာ Property အခု 50 ရပါတယ်။
