# Schema & Model
![mongoDB](https://github.com/yooooonk/TIL/blob/master/img/mongodb.png)

``` javascript
const mongoose = require('mongoose')
const productSchema = new mongoose.Schema({
    name:{
        type:String,
        required:true
    },
    description:{
        type:String,
        required:true
    },
    price:{
        type:Number
    }
})

const Product = mongoose.model('Product',productSchema)

module.exports = Product;
```