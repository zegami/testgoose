# Model Mock
Mock of Mongoose [Model](http://mongoosejs.com/docs/api.html#model-js). To get your module under test to require it instead of the real Mongoose Model, use [proxyquire](https://github.com/thlorenz/proxyquire):
```javaScript
const proxyquire = require('proxyquire').noCallThru();
const testgoose = require('testgoose');

const TaskMock = testgoose.model.mock();
// Define mock behavior

const taskController = proxyquire('../controllers/task', { '../models/task': TaskMock } );
// Call the function under test and make assertions
```

You must specify `withArgs()` on each function that you expect the mock to be called with. This extends to queries as well.

The mock will throw an error in the system under test if it is invoked differently than what was specified.


## find.withArgs()...returns()
Define the data returned from Mongoose [Model.find](http://mongoosejs.com/docs/api.html#model_Model.find).

##### Parameters
- `err` **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** error to be returned by the find callback
- `docs` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)>** documents to be returned by the find callback

##### Example
```javascript
const testgoose = require('testgoose');
const ProductMock = testgoose.model.mock();
ProductMock.find.withArgs({name: 'banana'}).returns(new Error('something bad happened'), null);
```

```javascript
const testgoose = require('testgoose');
const ProductMock = testgoose.model.mock();
const productData = [
  { _id: '507f191e810c19729de860ea', name: 'banana' },
  { _id: '5a16602357c05c3a06a4dca8', name: 'orange' }
];
ProductMock.find.withArgs().returns(null, productData);
```

```javascript
const testgoose = require('testgoose');
const ProductMock = testgoose.model.mock();
ProductMock.find.withArgs({name: 'banana'}).sort.withArgs('-name').returns(new Error('something bad happened'), null);
```


## findById.withArgs()...returns()
Define the data returned from Mongoose [Model.findById](http://mongoosejs.com/docs/api.html#model_Model.findById).

##### Parameters
- `err` **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** error to be returned by the findById callback
- `doc` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** document to be returned by the findById callback

##### Example
```javascript
const testgoose = require('testgoose');
const UserMock = testgoose.model.mock();
UserMock.findById.withArgs(1234).returns(new Error('something bad happened'), null);
```

```javascript
const testgoose = require('testgoose');
const dataStub = { _id: '507f1f77bcf86cd799439011', firstName: 'Sally', lastName: 'Saltwater' };
const UserMock = testgoose.model.mock();
UserMock.findById.withArgs(dataStub._id).returns(null, dataStub);
```

```javascript
const testgoose = require('testgoose');
const UserMock = testgoose.model.mock();
UserMock.findById.withArgs('507f1f77bcf86cd799439011').select.withArgs('firstName').returns(null, { firstName: 'Sally' });
```


## findByIdAndRemove.withArgs()...returns()
Define the data returned from Mongoose [Model.findByIdAndRemove](http://mongoosejs.com/docs/api.html#model_Model.findByIdAndRemove).

##### Parameters
- `err` **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** error to be returned by the findByIdAndRemove callback
- `doc` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** document to be returned by the findByIdAndRemove callback

##### Example
```javascript
const testgoose = require('testgoose');
const UserMock = testgoose.model.mock();
UserMock.findByIdAndRemove.withArgs('507f1f77bcf86cd799439011').returns(new Error('something bad happened'), null);
```

```javascript
const testgoose = require('testgoose');
const UserMock = testgoose.model.mock();
UserMock
  .findByIdAndRemove.withArgs('507f1f77bcf86cd799439011')
  .returns(null, { _id: '507f1f77bcf86cd799439011', firstName: 'Sally', lastName: 'Saltwater' });
```

```javascript
const testgoose = require('testgoose');
const UserMock = testgoose.model.mock();
UserMock
  .findByIdAndRemove.withArgs('507f1f77bcf86cd799439011')
  .select.withArgs('firstName')
  .returns(null, { firstName: 'Sally' });
```


## findByIdAndUpdate.withArgs()...returns()
Define the data returned from Mongoose [Model.findByIdAndUpdate](http://mongoosejs.com/docs/api.html#model_Model.findByIdAndUpdate).

##### Parameters
- `err` **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** error to be returned by the findByIdAndUpdate callback
- `doc` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** document to be returned by the findByIdAndUpdate callback

##### Example
```javascript
const testgoose = require('testgoose');
const UserMock = testgoose.model.mock();
UserMock
  .findByIdAndUpdate.withArgs('507f1f77bcf86cd799439011', { firstName: 'Samuel' })
  .returns(new Error('something bad happened'), null);
```

```javascript
const testgoose = require('testgoose');
const UserMock = testgoose.model.mock();
UserMock
  .findByIdAndUpdate.withArgs('507f1f77bcf86cd799439011', { firstName: 'Samuel' })
  .returns(null, { _id: '507f1f77bcf86cd799439011', firstName: 'Samuel', lastName: 'Saltwater' });
```

```javascript
const testgoose = require('testgoose');
const UserMock = testgoose.model.mock();
UserMock
  .findByIdAndUpdate.withArgs('507f1f77bcf86cd799439011', { firstName: 'Samuel' })
  .select.withArgs('firstName')
  .returns(null, { firstName: 'Samuel' });
```


## prototype.save.withArgs()...returns()
Define the data returned from Mongoose [Model#save](http://mongoosejs.com/docs/api.html#model_Model-save).

##### Parameters
- `err` **[Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)** error to be returned by the save callback
- `doc` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** document to be returned by the save callback

##### Example
```javascript
const testgoose = require('testgoose');
const CarMock = testgoose.model.mock();
CarMock.prototype.save.withArgs().returns(new Error('something bad happened'), null);
```

```javascript
const testgoose = require('testgoose');
const TaskMock = testgoose.model.mock();
CarMock.prototype.save.withArgs().returns(null, { vin: '1B7HC16Z6SS365053', color: 'viper red' });
```