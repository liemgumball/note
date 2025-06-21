==**Jest**== is an open source ==**JavaScript**== testing framework developed by ==**Facebook**==. It's commonly  
used to test ==**React**== code, but can also be used to test ==**Node.js**== applications.

> [!info] Jest  
> Jest is a delightful JavaScript Testing Framework with a focus on simplicity.  
> [http://jestjs.io](http://jestjs.io)  

### Target

- Getting start with ==**Jest**==
- Mocking concept
- Testing with [[MongoDB]]

```JavaScript
const uppercase = require('../uppercase')

describe('uppercase', () => {
	test('should uppercase the string', () => {
		expect(uppercase('hello')).toBe('HELLO')
	})
})
```

## Mock function

==Mock functions== allow you to test the links between code by erasing the actual implementation of a function.

There are two ways to mock functions

- Creating a mock function to use in test code
- Writing a manual mock to override a module dependency

```JavaScript
const forEach = require('./forEach');

const mockCallback = jest.fn(x => 42 + x);

test('forEach mock function', () => {
  forEach([0, 1], mockCallback); // run callback() in loop

  // The mock function was called twice
  expect(mockCallback.mock.calls).toHaveLength(2);

  // The first argument of the first call to the function was 0
  expect(mockCallback.mock.calls[0][0]).toBe(0);

  // The first argument of the second call to the function was 1
  expect(mockCallback.mock.calls[1][0]).toBe(1);

  // The return value of the first call to the function was 42
  expect(mockCallback.mock.results[0].value).toBe(42);
});
```

### Mock return value

```JavaScript
const myMock = jest.fn();
console.log(myMock());
// > undefined

myMock.mockReturnValueOnce(10).mockReturnValueOnce('x').mockReturnValue(true);

console.log(myMock(), myMock(), myMock(), myMock());
// > 10, 'x', true, true
```

### Mocking Module

```JavaScript
import axios from 'axios';

class Users {
  static all() {
    return axios.get('/users.json').then(resp => resp.data);
  }
}

export default Users;
```

Mock the module we can provide a `mockResolvedValue` for `.get` that returns the data we want

```JavaScript
import axios from 'axios';
import Users from './users';

jest.mock('axios');

test('should fetch users', () => {
  const users = [{name: 'Bob'}];
  const resp = {data: users};
  axios.get.mockResolvedValue(resp);

  // or you could use the following depending on your use case:
  // axios.get.mockImplementation(() => Promise.resolve(resp))

  return Users.all().then(data => expect(data).toEqual(users));
});
```

> [!info] Mock Functions · Jest  
> Mock functions allow you to test the links between code by erasing the actual implementation of a function, capturing calls to the function (and the parameters passed in those calls), capturing instances of constructor functions when instantiated with new, and allowing test-time configuration of return values.  
> [https://jestjs.io/docs/mock-functions#mock-implementations](https://jestjs.io/docs/mock-functions#mock-implementations)  

> [!info] How To Mock Fetch in Jest  
> Making HTTP requests in tests isn't a great idea in most situations.  
> [https://www.leighhalliday.com/mock-fetch-jest](https://www.leighhalliday.com/mock-fetch-jest)  

## Jest with MongoDB

1. Install modules
    
    ```JavaScript
    npm install -D @shelf/jest-mongodb
    npm install mongodb
    ```
    
2. Specify jest `preset`
    
    ```JavaScript
    /** @type {import('jest').Config} */
    const config = {
    	preset: '@shelf/jest-mongodb',
    	verbose: true,
    }
    
    module.exports = config
    ```
    
3. Write test (there's no need to load any dependencies)
    
    ```JavaScript
    const {MongoClient} = require('mongodb');
    
    describe('insert', () => {
      let connection;
      let db;
    
      beforeAll(async () => {
        connection = await MongoClient.connect(globalThis.__MONGO_URI__, {
          useNewUrlParser: true,
          useUnifiedTopology: true,
        });
        db = await connection.db(globalThis.__MONGO_DB_NAME__);
      });
    
      afterAll(async () => {
        await connection.close();
      });
    
      it('should insert a doc into collection', async () => {
        const users = db.collection('users');
    
        const mockUser = {_id: 'some-user-id', name: 'John'};
        await users.insertOne(mockUser);
    
        const insertedUser = await users.findOne({_id: 'some-user-id'});
        expect(insertedUser).toEqual(mockUser);
      });
    });
    ```