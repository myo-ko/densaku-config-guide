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
3. create account နှိပ်လိုက်ပါ။ ဒီအကောင့်က GA account ကိုပြောတာဖြစ်ပါတယ်။
4. account name ထည့်ပါ။ ကျန်တာဒီတိုင်းထားပြီး Next နှိပ်ပါ။<br>
	<img src="images/ga-setup-1.png"><br>
5. Web ကိုပဲထားပြီး Next နှိပ်ပါ။
 	<img src="images/ga-setup-2.png">
6. Property Setup ရောက်ပါပြီ။
	- Website Name: ကိုကြိုက်တာပေးပါ။
	- Website URL: den-saku url ထည့်ပါ။ local ဆို 127.0.0.1 ဆိုပြီးပဲထည့်ပါ။
	- Industry Category: Shopping ပဲရွေးလိုက်ပါ။
	- Reporting Time Zone: real site အတွက် Japan ရွေးပါ။ local ဆို Myanmar time ပဲရွေးလိုက်ပါ။
	- Create နှိပ်ပါ။
	<img src="images/ga-setup-2.png">
7. Term of Service တွေ၊ User Agreement တွေကို Accpet လုပ်ပြီး အောက်ဆုံးက I Accept button ကိုနှိပ်ပါ။
8. အောက်ပုံကျလာပါမယ်။ GA account တစ်ခုနဲ့ Property တစ်ခုတည်ဆောက်လို့ပြီးပါပြီ။ **Tracking ID** ကို Copy ကူးပြီး notepad ပေါ်ခဏတင်ထားလိုက်ပါ။
	<img src="images/ga-setup-4.png">
9. အပေါ်အစိမ်းရောင်အဝိုင်းကို select လုပ်ပြီး ကျွန်တော်တို့ GA အကောင့်တွေ Property တွေကို ပြောင်းကြည့်လို့ရပါတယ်။
10. Google အကောင့်တစ်ခုအတွက် GA အကောင့် ၁၀ ခုရပါတယ်။ GA အကောင့် ၁ခုမှာ Property အခု 50 ရပါတယ်။

## GTM စတင်သုံးစွဲခြင်း

1. https://tagmanager.google.com သို့သွားပါ။
2. အကောင့်တစ်ခု အသစ်လုပ်ပါ။
3. အောက်ပါပုံနဲ့တူတဲ့ Form တစ်ခုရလာပြီဆို data ဖြည့်ပါ။
	- Account name: အဆင်ပြေတာရပါတယ်။
	- Country: production ရောက်ရင်တော့ Japan လုပ်ထားလိုက်ပါ။ local ဆိုရင် US ပဲထည့်လိုက်ပါ။
	- Container name: production ရောက်ရင် website လိပ်စာအမှန်ထည့်လိုက်ပါ။ local ဆိုတော့ အဆင်ပြေတာထည့်ပါ။
	- Target Platform: Web ကိုပဲရွေးပါ။
	- Create button ကိုနှိပ်ပါ။
	<img src="images/gtm-setup-1.png">
4. Workspace manage လုပ်တဲ့ page ကိုရောက်သွားပါမယ်။
	<img src="images/gtm-setup-2.png">
	**Container ID** တွေကို ဂရုစိုက်ပါ။ အဲ့ဒါတွေက အတူတူပဲဖြစ်ရပါမယ်။
5. အပေါ်ပိုင်းက code တွေကို  `default_frame.twig` ဖိုင်ထဲမှာ ထည့်ရပါမယ်။ *(ဒီနေရာကစပြီး EC-Cube ရဲ့ Source code တွေကိုပြင်ပါတော့မယ်)*
6. `default_frame.twig` ဟာနေရာ ၂ခုမှာရှိတတ်ပါတယ်။ `src/Eccube/Resource/template/default` နဲ့ `app/template/default` အောက်မှာတွေပါ။ `app/template/default` ကို ဦးစားပေးယူပါတယ်။ EC-Cube ရဲ့ Documentation အရ ကိုယ်ပိုင် template သုံးမယ်ဆိုရင် `app/template` အောက်မှာပဲသွားရေးပါလို့ ပြောထားပါတယ်။ `app/template` ထဲမရေးဘဲ `src/Eccube/Resource` အောက်က ဖိုင်ကိုပဲသွားပြင်မယ်ဆိုဘာဖြစ်မလဲ? အဖြေကတော့ ဘာမှမဖြစ်ပါဘူး။ မိမိစိတ်ကြိုက်နေရာမှာသွားပြင်လို့ရပါတယ်။ 
7. အဆင့် ၄ မှာပြထားတဲ့ JavaScript အပေါ်ပိုင်းကို  `<head>` tag အဖွင့်ပြီးတဲ့နေရာမှာ ထည့်ရပါမယ်။
	<img src="images/gtm-setup-3.png">	
8. JavaScript အောက်ပိုင်းကိုတော့ `<body>` tag အဖွင့်ပြီးရင်ထည့်ရပါမယ်။
	<img src="images/gtm-setup-4.png">
9. ဒါဆိုတော့ Setup ပြီးသွားပြီဖြစ်ပါတယ်။

## အသေးစိတ်စီမံခန့်ခွဲခြင်း

GTM မှာ အပိုင်း ၃ ပိုင်းပါပါတယ်။ Trigger, Variable နဲ့ Tag တွေပါ။ Web page element တွေရဲ့ event တွေကို trigger ကစောင့်ကြည့်ပါတယ်။ ကျွန်တော်တို့ တည်ဆောက်ထားတဲ့ trigger ရဲ့ကွင်းစက်ထဲဝင်လာပြီဆိုတာနဲ့ အဲ့ trigger တွေက ဆိုင်ရာဆိုင်ရာ Tag တွေကို Event data တွေ ပေးပို့လိုက်မှာဖြစ်ပါတယ်။ အဲ့ data တွေက variable အနေနဲ့ Tag ကတစ်ဆင့် Third party service တွေဖြစ်တဲ့ Google Analytics တို့လို server တွေကိုရောက်လာပါတယ်။ အဲ့ variable တွေမှာ သူမှတ်ထားတဲ့ default variable တွေအပြင် ကျွန်တော်တို့ကိုယ်တိုင်သတ်မှတ်ထားတဲ့ varible ကိုပါ ပို့လို့ရပါတယ်။ အဲ့ဒါနဲ့ ကျွန်တော်တို့ဟာ Product data တွေကို ပို့မှာဖြစ်ပါတယ်။

### Product List Page ကို စီမံခန့်ခွဲခြင်း

1. GTM Dashboard ကနေ Triggers ကို သွားလိုက်ပါ။
	<img src="images/product-list-tag-1.png">
2. New button ကိုနှိပ်ပြီး Trigger အသစ်လုပ်လိုက်ပါ။
3. အောက်ပါအတိုင်း Setting ပေးလိုက်ပါ။
	- Trigger နာမည်ကို ကြိုက်တာပေးပါ။
	- Trigger Type: Page View
	- This trigger fires on: Some Page Views
	- Page Path: contains: products/list
	- Save ကိုနှိပ်ပါ။
	<img src="images/product-list-tag-2.png">
4. GTM Dashboard ကနေ Tags ကို သွားလိုက်ပါ။
5. New button ကို နှိပ်လိုက်ပါ။
6. အောက်ပါအတိုင်း Setting ပေးလိုက်ပါ။
	- Tag နာမည်ကို ကြိုက်တာပေးပါ။
	- Tag Configuration အောက်က Icon ဝိုင်းဝိုင်းကို နှိပ်ပါ။
		<img src="images/product-list-tag-3.png">
	- Google Analytics: Universal Analytics ကိုရွေးပါ။
	- Track Type: Event ကိုရွေးလိုက်ပါ။
	- Category: **ဒီမှာ ကျွန်တော်ကတော့ page action ကိုရေးလိုက်ပါတယ်။ ဒီစာသားအတိုင်း GA မှာသွားပေါ်တာဖြစ်လို့ ဒီမှာ အသေအချာရေးရပါမယ်။ Production site ရောက်ရင်တော့ Japan လို description ရေးမှာဖြစ်ပါတယ်။ လောလောဆယ်တော့ English လိုပဲ ရေးထားလိုက်ပါတယ်။**
		<img src="images/product-list-tag-4.png">
	- Action: အဆင့် ၅ အတိုင်းပါပဲ။ လောလောဆယ်တော့ Product List view ဆိုပြီးပဲ ရေးထားပါတယ်။
	- Label, value, non-interaction hit တွေကို ဒီတိုင်းပဲထားပါမယ်။
	- Google Analytics Settings: မှာ New variable ဆိုတာကို ရွေးလိုက်ပါ။ Dialog ထပ်ထွက်လာပါမယ်။
		<img src="images/product-list-tag-5.png">
	- Variable name ကိုအဆင်ပြေတာပေးပါ။ ပြီးရင် Google Analytics ကို စတင်သုံးစွဲတုန်းက **Tracking ID** ကိုထည့်ပေးရမှာဖြစ်ပါတယ်။
	- ပြီးရင် Save ကိုနှိပ်ပါ။
	- Triggering အောက်က Icon ဝိုင်းဝိုင်းကို နှိပ်ပါ။ 
	- ပြီးရင် အဆင့် ၃ တုန်းက လုပ်ခဲ့တဲ့ Trigger ကိုရွေးလိုက်ပါ။
	- ပြီးရင် Save ကိုနှိပ်ပါ။
7. Dashboard ရဲ့ ညာဘက်အပေါ်မှာ Submit button ကို နှိပ်လိုက်ပါ။
8. ဘာမှမရေးဘဲ Publish button ကိုနှိပ်ပါ။
9. Continue ကို ထပ်နှိပ်ပါ။
10. Version နံပါတ်အသစ်နဲ့ commit တစ်ခုပြီးသွားပါပြီ။
11. Workspace tab ကိုပြန်သွားပါ။
12. Dashboard ရဲ့ ညာဘက်အပေါ်မှာ Preview button ကို နှိပ်လိုက်ပါ။ Tag manager ရဲ့ Debug mode ရောက်နေပါပြီ။
	<img src="images/product-list-tag-6.png">
13. Browser Tab အသစ်ဖွင့်ပြီး `localhost/densaku/products/list` ဆိုပြီးရိုက်ထည့်ကြည့်ပါ။
14. အောက်ကလို Tag Manager ဆိုပြီး debug panel ကျလာပါတယ်။ အဲ့မှာ Page ရဲ့ ဘယ်အချိန်မှာ ဘယ် Tag တွေ Fire ဖြစ်သွားသလဲဆိုတာတွေ့ရမှာပါ။
	<img src="images/product-list-tag-7.png">
15. https://analytics.google.com သို့သွားပါ။
16. ဘယ်ဘက်က navigation menu ကနေ Realtime > Events သို့သွားပါ။
17. Event Category column အောက်မှာ ကျွန်တော်တို့ Tag ဆက်တင်ချိန်တုန်းက ပေးခဲ့တဲ့ Property တွေပါလာတာ တွေ့ပါလိမ့်မယ်။
	<img src="images/product-list-tag-8.png">




