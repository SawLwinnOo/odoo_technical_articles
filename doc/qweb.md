<h1>Qweb Template</h1>

Python ရဲ့ frameworks တွေဖြစ်တဲ့ Flask နှင့် Django မှာ contents တွေကို generate လုပ်ဖို့ jinja template ကို အသုံးပြုသလို odoo မှာကတော့ qweb template engine ကိုအသုံးပြုပါတယ်။ qweb ဟာ xml base ဖြစ်ပြီးတော့ odoo database ရဲ့ model expression, fields တွေကို အသုံးပြုပြီး dynamic content တွေအဖြစ် generate လုပ်နိုင်ပါတယ်။ qwebမှာ statements ကို ရှေ့ဆက် t- ကို အသုံးပြုပြီး attributes အနေနဲ့ elements တွေမှာ ထည့်သွင်းအသုံးပြုပါတယ် Directives လို့လည်းခေါ်ပါတယ်။
```qweb
<t t-if="condition">
    <p>Hello World</p>
</t>
```


အထက်ပါ ဥပမာဆိုရင် condition သာမှန်ခဲ့ရင် output အနေနဲ့ ```<p>Test</p>``` ရရှိမှာပါ ဘာလိုလဲဆိုတော့ t element ဟာ qweb ရဲ့ placeholder element ဖြစ်တာကြောင့် t element အတွင်းမှာရှိတဲ့ အခြား element တွေကိုသာ output ထုတ်ပေးတာဖြစ်ပါတယ်။တခြား template engine တွေလိုပဲ looping , condition statements တွေကိုလည်း support ပေးပါတယ်။ qweb မှာ t-if, t-elif, t-else ဆိုပြီး condition directives တွေရှိပါတယ်။
```qweb
<div>
	<p t-if="user.birthday == today()">Happy birthday!</p>
	<p t-elif="user.login == 'root'">Welcome master!</p>
	<p t-else="">Welcome!</p>
</div>
```

အထက်ပါ ဥပမာဆိုရင် ပထမ condition သာမှန်ရင် နောက် conditions တွေဆက်မလုပ်တော့ပဲ ပထမတစ်ခုသာ output ထုတ်ပေးမှာဖြစ်ပါတယ်။ ကျနော်တို့ ပုံမှန် conditions တွေရေးရတာနဲ့ ပုံစံတူပါတယ်။loop အနေနဲ့ t-foreach directives ကို အသုံးပြုပါတယ်။ foreach ဟာလည်း ကျနော်တို့ for loop ရေးတဲ့ ပုံစံမျိုးဖြစ်ပါတယ်။ current state ကို ဖော်ပြဖို့ အတွက် second parameter အနေနဲ့ t-as directive ကိုအသုံးပြုပါတယ်။ odoo js owl library မှာဆိုရင်တော့  t-as parameter နောက်မှာ t-key parameter ကိုထည့်ပေးရပါတယ် python မှာတော့ မလိုပါဘူး။

eg.1

```
<t t-foreach="[1, 2, 3]" t-as="i" >
    	<p><t t-out="i"/></p>
</t>
```
eg.2
```
<p t-foreach="[1, 2, 3]" t-as="i" >
   	 <t t-esc="i"/>
</p>
```
Output: 
```
<p>1</p>
<p>2</p>
<p>3</p>
```
Example နှစ်ခုလုံးမှာဆိုရင် ရေးပုံမတူကြပေမယ့် output အတူတူရမှာဖြစ်ပါတယ်။ output အတွက် t-out directive ကို အသုံးပြုနိုင်သလို t-esc ကိုလည်းအသုံးပြုနိုင်ပါတယ်။ ကွာခြားချက်ကိုတော့ owl library ရဲ့ documentation မှာ အသေးစိတ်သွားလေ့လာနိုင်ပါတယ်။ ကျနော်တို့ ပုံမှန် xml attribute တွေသတ်မှတ်သလိုပဲ qweb မှာလည်း t-att directive ကို အသုံးပြုပြီး attribute node တွေကို compute လုပ်ပေးနိုင်ပါတယ်။ t-att directive မှာ t-att-$name,  t-attf-$name, t-att=mapping ဆိုပြီး ၃ မျိုးရှိပါတယ်။

Example for t-att-name
```
    <div t-att-name="Hello"/>
```
Output : ```<div name="Hello"></div>```

Example for t-attf-$name
```
<t t-foreach="[1, 2, 3]" t-as="item">
    <li t-attf-class="row {{ (item_index % 2 === 0) ? 'even' : 'odd' }}">
        <t t-out="item"/>
    </li>
</t>
```
Output:
```
<li class="row even">1</li>
<li class="row odd">2</li>
<li class="row even">3</li>
```
Example for t-att-mapping
```
<div t-att="{'a': 1, 'b': 2}"/>
```
Output: ```<div a="1" b="2"></div>```

Qweb မှာ t-set directive ကို အသုံးပြုပြီး variable တွေသတ်မှတ်ပြီး အသုံးပြုနိုင်ပါသေးတယ်။ စိတ်ဝင်စားလို့ အသေးစိတ်သိချင်တယ် ဆိုရင်တော့ အောက်မှာပေးထားတဲ့ links တွေကနေ အခြားအကြောင်းရာသစ်တွေပါ ထပ်မံ ဝင်ရောက်လေ့လာနိုင်ပါတယ်ဗျ။ နားလည်သလိုချရေးထားတာဖြစ်တဲ့ အတွက် အမှားတွေပါခဲ့ရင်လည်း ပြင်ပေးခဲ့ကြပါဦးဗျ။

Odoo qweb - https://www.odoo.com/documentation/16.0/developer/reference/frontend/qweb.html

Owl Template- https://github.com/odoo/owl/blob/master/doc/reference/templates.md
