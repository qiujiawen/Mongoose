# Scheme
schema是mongoose里会用到的一种数据模式，可以理解为表结构的定义；每个schema会映射到mongodb中的一个collection，它不具备操作数据库的能力。

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;
const UserSchema = new Schema({
    username: String, // 用户名
    password: String, // 密码
});
module.exports = UserSchema;
```

### SchemaTypes 数据类型

数据类型用于定义默认路径， 验证方式， 获取/设置方法，用于数据库查询的默认字段，以及其他针对字符串与数字的特性。

##### Mongoose中所有可用的数据类型

+ String 字符串

+ Number 数字

+ Date 日期

+ Buffer 缓冲区

+ Boolean 布尔值

+ Mixed 混合

+ Objectid 对象ID

+ Array 数组

##### expmale
```
var Schema = new Schema({
    name: String,
    binary: Buffer,
    isDeleted: Boolean,
    updated: Date,
    age: Number,
    mixed:Schema.Types.Mixed,
    _id:Schema.Types.ObjectId,  //主键
    _fk:Schema.Types.ObjectId,  //外键
    array: [],
    arrOfString: [String],
    arrOfNumber: [Number],
    arrOfDate: [Date],
    arrOfBuffer: [Buffer],
    arrOfBoolean: [Boolean],
    arrOfMixed: [Schema.Types.Mixed],
    arrOfObjectId: [Schema.Types.ObjectId],
    nested:{
        stuff: String,
    }
})
```

Buffer 和 ArrayBuffer 是 Nodejs 两种隐藏的对象(<a href='http://nodejs.cn/api/buffer.html'>相关链接</a>)

##### Schema.Type.Mixed

Schema.Types.Mixed 是 Mongoose 定义的混合类型，该混合类型如果未定义具体形式，是一种“存啥都行”的数据类型

两者是相等的：
```
let AnySchema = new Schema({any:{}})
let AnySchema = new Schema({any:Schema.Types.Mixed})
```

混合类型因为没有特定约束，因此可以任意修改，一旦修改了原型，则必须调用markModified()

```
person.anything = {x:[3,4,{y:'change'}]}
person.markModified('anything')  //传入anything，表示该属性类型发生变化
person.save()
```

##### ObjectId

对象ID同MongoDB内置的_id 的类型。由24位Hash字符串；可以用Schema.Types.ObjectId 来声明一个对象ID类型。

```
let mongoose = require('mongoose')
let ObjectId = mongoose.Schema.Types.ObjectId
let StudentSchema = new Schema({})   //默认会有_id:ObjectId
let TeacherSchema = new Schema({id:ObjectId})  //只有id:ObjectId
```
##### Array
下面代码是等价：
```
var Empty1 = new Schema({ any: [] });
var Empty2 = new Schema({ any: Array });
var Empty3 = new Schema({ any: [Schema.Types.Mixed] });
var Empty4 = new Schema({ any: [{}] });
```

##### 参数查询

　　$or　　　　或关系

　　$nor　　　 或关系取反

　　$gt　　　　大于

　　$gte　　　 大于等于

　　$lt　　　　 小于

　　$lte　　　  小于等于

　　$ne            不等于

　　$in             在多个值范围内

　　$nin           不在多个值范围内

　　$all            匹配数组中多个值

　　$regex　　正则，用于模糊查询

　　$size　　　匹配数组大小

　　$maxDistance　　范围查询，距离（基于LBS）

　　$mod　　   取模运算

　　$near　　　邻域查询，查询附近的位置（基于LBS）

　　$exists　　  字段是否存在

　　$elemMatch　　匹配内数组内的元素

　　$within　　范围查询（基于LBS）

　　$box　　　 范围查询，矩形范围（基于LBS）

　　$center       范围醒询，圆形范围（基于LBS）

　　$centerSphere　　范围查询，球形范围（基于LBS）

　　$slice　　　　查询字段集合中的元素（比如从第几个之后，第N到第M个元素）

```
User.find({userage: {$gte: 21, $lte: 65}}, callback);    //这表示查询年龄大于等21而且小于等于65岁
```