# Restaurant API

Restaurant Management System ရဲ့ Backend အပိုင်းမှာ နေရာကျပါတယ်။ TypeScript Language နဲ့ Nest JS Framework ကို အသုံးပြုထားပါတယ်။ 

ကောင်တာအသုံးပြုသူတွေကော၊ စာပွဲထိုးလေးတွေကော၊ ဆိုင်ပိုင်ရှင်ပါ မတူညီတဲ့ Platform တွေကနေ ဒီ System ကို အသုံးပြုကြပါမယ်။ ဘယ်လို Platform ကပဲဖြစ်ဖြစ် ဘယ်လို Language ပဲဖြစ်ဖြစ် တူညီတဲ့ Resource တွေကို Support လုပ်ပေးဖို့အတွက် ဒီ Project မှာ တာဝန်ရှိပါတယ်။ 

## Architecture

![Architecture](/images/arch.png)

### Persistance Layer

Entity တွေဟာ Relational Database ထဲက  Table တွေနဲ့ Map လုပ်ထားတဲ့ Object တွေဖြစ်ပါတယ်။ တဖန် Nest JS Type Orm ကို အသုံးပြုမယ်ဆိုရင် Database Operation တွေကို အလွယ်တကူအသုံးပြုနိုင်အောင် Repository Object တွေကို လိုအပ်သလို Inject လုပ်ပြီး အသုံးပြုနိုင်မှာ ဖြစ်ပါတယ်။ 

Entity တွေဟာ Table တွေကို ကိုယ်စားပြုတဲ့ Object တွေဖြစ်ကြပြီး Repository တွေက Database Operation တွေကို ဆောင်ရွက်ပေးနိုင်တဲ့ Object တွေ ဖြစ်ကြပါတယ်။

### Business Logic Layer

အထက်ပါ Diagram ထဲမှာပါဝင်တဲ့ Services တွေဟာ Business Logic Layer မှာ တာဝန်ကျပါတယ်။ ပြန်ပြီး အသုံးပြုနိုင်တဲ့ Business Logic တွေကို Wrap လုပ်ပေးမယ်၊ ပြီးတော့ Repository တွေကို အသုံးပြုပြီး Business Logic အလိုက် Prensation Layer အတွက် Data တွေကို Support လုပ်ပေးမယ်။ Presentation Layer ကနေ ရလာတဲ့ User Input Data တွေကိုနဲ့ Repository ကို အသုံးပြုပြီး Persistance Data တွေကို Update လုပ်ပေးပါမယ်။

Business Logic ကို ရေးသားကြတဲ့နေရာမှာ တူညီတဲ့ အပိုင်းတွေရှိနိုင်ပါတယ်။ Resource တွေကို ID နဲ့ရှာတာတို့။ Resource တွေအားလုံးကို ရှာတာတို့၊ Resource တွေကို Insert, Update, Delete လုပ်တာတို့ တူညီတဲ့ လုပ်ဆောင်မှုတွေရှိနေနိုင်ပါတယ်။ အဲ့ဒီအတွက် Generic Base Class လေးတွေကို ရေးသားထားပါတယ်။ Service Class တွေက သက်ဆိုင်ရာ Base Class ကို Extend လုပ်ထားပြီး Specific Logic တွေကိုပဲ မိမိအထဲမှာ ရေးသားသွားမှာ ဖြစ်ပါတယ်။

[IdEnable](https://github.com/minlwin/the-restaurant/blob/master/restaurant-api/src/common/id.enable.ts)
```.typescript
export interface IdEnable extends ObjectLiteral{
    id:number
}
```

[BaseService](https://github.com/minlwin/the-restaurant/blob/master/restaurant-api/src/common/base.controller.ts)
```typescript
export class BaseService<T extends IdEnable> {

    constructor(protected readonly repo:Repository<T>) {}

    findAll() {
        return this.repo.find()
    }

    findById(id:number) {
        return this.repo.findOne(id)
    }
}
```
[BaseServiceMutable](https://github.com/minlwin/the-restaurant/blob/master/restaurant-api/src/common/base.controller.mutable.ts)
```typescript
export class BaseServiceMutable<T extends IdEnable> extends BaseService<T> {

    constructor(repo:Repository<T>) {
        super(repo)
    }

    save(t:T) {
        return this.repo.save(t)
    }
}
```

### Presentation Layer 


## Data Structure
Database အနေနဲ့ကတော့ Open Source Database ဖြစ်တဲ့ MariaDB ကို အသုံးပြုသွားပါမယ်။ Nest JS Framework မှာ Relational Database ကို အသုံးပြုဖို့အတွက် TypeORM Framework ကို အသုံးပြုသွားမှာဖြစ်ပါတယ်။

TypeORM ဆိုတာ Object Relation Mapping (ORM) ကို အခြေခံထားတဲ့ Framework တစ်ခုဖြစ်ပါတယ်။ Nest JS မှာ TypeORM ကို အသုံးပြုနိုင်အောင် ပြင်ဆင်ပေးထားပါတယ်။

ဒီီ System မှာ အသုံးပြုမည့် Database Structure (ERD) ကတော့ အောက်ပါအတိုင်းဖြစ်ပါတယ်။ 

![ERD](/images/RestaurantERD.png)

## Modules

Nest JS ဟာ Type Script ကို အသုံးပြုထားတဲ့ အတွက် ရည်ရွယ်ချက်အပေါ်မူတည်ပြီး Module တွေကို ခွဲခြားရေးသားနိုင်ပါတယ်။
လက်ရှိ System မှာတော့ အောက်ပါအတိုင်း Module တွေကိို ခွဲခြားရေးသားထားပါတယ်။

1. [Employee Module](1.Employee.md)
2. [Master Module](2.Master.md)
3. [Sale Module](3.Sale.md)


