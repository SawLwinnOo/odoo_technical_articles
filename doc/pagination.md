<h1>Pagination in Odoo</h1>

How to add Pagination in odoo

Pagination ဆိုတာ ပုံစံတူတဲ့ contents တွေ pages တွေကို အစီစဥ်အလိုက် တွဲဆက်ပေးတာကို ခေါ်ပါတယ်။ e-commerce site တစ်ခုရဲ့ page တစ်ခုမှာ products တွေကို category တစ်ခုထဲမှာ ဖော်ပြချင်တဲ့အခါ သုံးပါတယ်။ odoo မှာ pagination ကို default feature တစ်ခုအနေနဲ့ ထည့်ပေးထားပြီး odoo controller ကနေ page rendering လုပ်တဲ့အခါ paganation values အနေနဲ့ ထည့်ပေးရပါတယ်။ 
```
pager = http.request.website.pager(
url='/path',
total=total,
page=page,
step=3,
)
```
အထက်ပါ ဥပမာဆိုရင် odoo ရဲ့ http.requset.website module ကနေ pager method ကိုခေါ်သုံးထားထားပါ။ pager method မှာ သုံးနိုင်တဲ့ parameters တွေကတော့ url, total, page, step, scope, url_args တို့ဖြစ်ပါတယ်။ url ကတော့ page url ဖြစ်ပါတယ်။ total ကတော့ ဥပမာ product model ဆိုရင် model table မှာရှိတဲ့ products အားလုံးရဲ့ အရေအတွက်ဖြစ်ပါတယ်။ page ကတော့ current page ဖြစ်ပြီး step ကတော့ pager page တစ်ခုမှာ ဖော်ပြမယ် item အရေအတွက်ဖြစ်ပါတယ်။ scope ကတော့ pagination တစ်ခုမှာ ဖော်ပြမယ့် page အရေအတွက်ဖြစ်ပါတယ်။ 
အသေးစိတ် ဥပမာတွေနဲ့ ရှင်းပြထားတာကို ဒီ  [links](https://www.cybrosys.com/blog/how-to-add-pagination-odoo-website) မှာသွားဖတ်နိုင်ပါတယ်။ ချရေးလိုက်တာက ကျနော့်ကို ပိုမှတ်မိစေတာမို့ hangout ရေးထားတာတွေပါ။ အမှားတွေပါရင်လည်း ပြင်ပေးခဲ့နိုင်ပါတယ်။

References-
https://www.cybrosys.com/blog/how-to-add-pagination-odoo-website

https://www.odoo.com/de_DE/forum/hilfe-1/pagination-on-website-custom-151094
