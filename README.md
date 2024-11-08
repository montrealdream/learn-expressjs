# RESTful API Node Server Boilerplate

[![Build Status](https://travis-ci.org/hagopj13/node-express-boilerplate.svg?branch=master)](https://travis-ci.org/hagopj13/node-express-boilerplate)
[![Coverage Status](https://coveralls.io/repos/github/hagopj13/node-express-boilerplate/badge.svg?branch=master)](https://coveralls.io/github/hagopj13/node-express-boilerplate?branch=master)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

Một dự án mẫu/khởi đầu để xây dựng nhanh các API RESTful bằng Node.js, Express và Mongoose.

Chỉ cần chạy một lệnh, bạn sẽ cài đặt được ứng dụng Node.js sẵn sàng cho sản xuất và cấu hình đầy đủ trên máy của mình. Ứng dụng đi kèm nhiều tính năng tích hợp, chẳng hạn như xác thực bằng JWT, xác thực yêu cầu, kiểm tra đơn vị và tích hợp, tích hợp liên tục, hỗ trợ docker, tài liệu API, phân trang, v.v. Để biết thêm chi tiết, hãy kiểm tra danh sách tính năng bên dưới.

## Quick Start

Để tạo một dự án, bạn chỉ cần chạy:

```bash
npx create-nodejs-express-app <project-name>
```

Hoặc

```bash
npm init nodejs-express-app <project-name>
```

## Cài đặt thủ công

Nếu bạn vẫn muốn cài đặt thủ công, hãy làm theo các bước sau:

Clone the repo:

```bash
git clone --depth 1 https://github.com/hagopj13/node-express-boilerplate.git
cd node-express-boilerplate
npx rimraf ./.git
```

Cài đặt các phần phụ thuộc:

```bash
yarn install
```

Thiết lập các biến môi trường:

```bash
cp .env.example .env

# open .env and modify the environment variables (if needed)
```

## Mục lục

- [Tính năng](#features)
- [Câu lệnh](#commands)
- [Biến môi trường](#environment-variables)
- [Cấu trúc dự án](#project-structure)
- [Tài liệu API](#api-documentation)
- [Error Handling](#error-handling)
- [Validation](#validation)
- [Authentication](#authentication)
- [Authorization](#authorization)
- [Logging](#logging)
- [Custom Mongoose Plugins](#custom-mongoose-plugins)
- [Linting](#linting)

## Tính năng

- **NoSQL database**: [MongoDB](https://www.mongodb.com) object data modeling sử dụng [Mongoose](https://mongoosejs.com)
- **Authentication and authorization**: sử dụng [passport](http://www.passportjs.org)
- **Validation**: yêu cầu xác thực dữ liệu sử dụng [Joi](https://github.com/hapijs/joi)
- **Logging**: sử dụng [winston](https://github.com/winstonjs/winston) và [morgan](https://github.com/expressjs/morgan)
- **Testing**: kiểm tra unit và tích hợp sử dụng [Jest](https://jestjs.io)
- **Error handling**: cơ chế xử lý lỗi tập trung
- **Tài liệu API**: với [swagger-jsdoc](https://github.com/Surnet/swagger-jsdoc) và [swagger-ui-express](https://github.com/scottie1984/swagger-ui-express)
- **Process management**: quản lý tiến trình sử dụng [PM2](https://pm2.keymetrics.io)
- **Dependency management**: với [Yarn](https://yarnpkg.com)
- **Biến môi trường**: sử dụng[dotenv](https://github.com/motdotla/dotenv) and [cross-env](https://github.com/kentcdodds/cross-env#readme)
- **Security**: set security HTTP headers sử dụng [helmet](https://helmetjs.github.io)
- **Santizing**: sanitize request data against xss and query injection
- **CORS**: Cross-Origin Resource-Sharing enabled sử dụng [cors](https://github.com/expressjs/cors)
- **Compression**: gzip compression with [compression](https://github.com/expressjs/compression)
- **CI**: continuous integration with (tích hợp liên tục với) [Travis CI](https://travis-ci.org)
- **Docker support**
- **Code coverage**: using [coveralls](https://coveralls.io)
- **Code quality**: with [Codacy](https://www.codacy.com)
- **Git hooks**: with [husky](https://github.com/typicode/husky) and [lint-staged](https://github.com/okonet/lint-staged)
- **Linting**: with [ESLint](https://eslint.org) and [Prettier](https://prettier.io)
- **Editor config**: consistent editor configuration using [EditorConfig](https://editorconfig.org)

## Câu lệnh

Run dưới môi trường local:

```bash
yarn dev
```

Run dưới môi trường production:

```bash
yarn start
```

Testing:

```bash
# run all tests
yarn test

# run all tests in watch mode
yarn test:watch

# run test coverage
yarn coverage
```

Docker:

```bash
# run docker container in development mode
yarn docker:dev

# run docker container in production mode
yarn docker:prod

# run all tests in a docker container
yarn docker:test
```

Linting:

```bash
# run ESLint
yarn lint

# fix ESLint errors
yarn lint:fix

# run prettier
yarn prettier

# fix prettier errors
yarn prettier:fix
```

## Biến môi trường

Các biến môi trường có thể được tìm thấy và sửa đổi trong tệp `.env`. Chúng đi kèm với các giá trị mặc định sau:

```bash
# Port number
PORT=3000

# URL of the Mongo DB
MONGODB_URL=mongodb://127.0.0.1:27017/node-boilerplate

# JWT
# JWT secret key
JWT_SECRET=thisisasamplesecret
# Số phút sau đó mã thông báo truy cập hết hạn
JWT_ACCESS_EXPIRATION_MINUTES=30
# số ngày sau đó mã thông báo làm mới hết hạn
JWT_REFRESH_EXPIRATION_DAYS=30

# SMTP configuration options for the email service
# Để thử nghiệm, bạn có thể sử dụng dịch vụ SMTP giả như Ethereal: https://ethereal.email/create
SMTP_HOST=email-server
SMTP_PORT=587
SMTP_USERNAME=email-server-username
SMTP_PASSWORD=email-server-password
EMAIL_FROM=support@yourapp.com
```

## Cấu trúc dự án

```
src\
 |--config\         # Environment variables and configuration related things
 |--controllers\    # Route controllers (controller layer)
 |--docs\           # Swagger files
 |--middlewares\    # Custom express middlewares
 |--models\         # Mongoose models (data layer)
 |--routes\         # Routes
 |--services\       # Business logic (service layer)
 |--utils\          # Utility classes and functions
 |--validations\    # Request data validation schemas
 |--app.js          # Express app
 |--index.js        # App entry point
```

## Tài liệu API

Để xem danh sách các API khả dụng và thông số kỹ thuật của chúng, hãy chạy máy chủ và truy cập `http://localhost:3000/v1/docs` trong trình duyệt của bạn. Trang tài liệu này được tạo tự động bằng cách sử dụng các định nghĩa [swagger](https://swagger.io/) được viết dưới dạng chú thích trong các tệp tuyến đường.

### API Endpoints

Danh sách các tuyến đường có sẵn:

**Auth routes**:\
`POST /v1/auth/register` - register\
`POST /v1/auth/login` - login\
`POST /v1/auth/refresh-tokens` - refresh auth tokens\
`POST /v1/auth/forgot-password` - send reset password email\
`POST /v1/auth/reset-password` - reset password\
`POST /v1/auth/send-verification-email` - send verification email\
`POST /v1/auth/verify-email` - verify email

**User routes**:\
`POST /v1/users` - create a user\
`GET /v1/users` - get all users\
`GET /v1/users/:userId` - get user\
`PATCH /v1/users/:userId` - update user\
`DELETE /v1/users/:userId` - delete user

## Error Handling

Ứng dụng này có cơ chế xử lý lỗi tập trung.

Controllers should try to catch the errors and forward them to the error handling middleware (by calling `next(error)`). For convenience, you can also wrap the controller inside the catchAsync utility wrapper, which forwards the error.

```javascript
const catchAsync = require('../utils/catchAsync');

const controller = catchAsync(async (req, res) => {
  // this error will be forwarded to the error handling middleware
  throw new Error('Something wrong happened');
});
```

Phần mềm trung gian xử lý lỗi gửi phản hồi lỗi có định dạng sau:

```json
{
  "code": 404,
  "message": "Not found"
}
```

Khi chạy ở chế độ phát triển, phản hồi lỗi cũng chứa error stack.

Ứng dụng này có một lớp tiện ích ApiError mà bạn có thể đính kèm mã phản hồi và thông báo, sau đó gửi nó từ bất kỳ đâu (catchAsync sẽ bắt được nó).

Ví dụ, nếu bạn đang cố gắng lấy thông tin người dùng từ DB nhưng không tìm thấy và bạn muốn gửi lỗi 404, mã sẽ trông giống như sau:

```javascript
const httpStatus = require('http-status');
const ApiError = require('../utils/ApiError');
const User = require('../models/User');

const getUser = async (userId) => {
  const user = await User.findById(userId);
  if (!user) {
    throw new ApiError(httpStatus.NOT_FOUND, 'User not found');
  }
};
```

## Validation

Dữ liệu yêu cầu được xác thực bằng [Joi](https://joi.dev/). Kiểm tra [tài liệu](https://joi.dev/api/) để biết thêm chi tiết về cách viết schema xác thực Joi.

The validation schemas are defined in the `src/validations` directory and are used in the routes by providing them as parameters to the `validate` middleware.

```javascript
const express = require('express');
const validate = require('../../middlewares/validate');
const userValidation = require('../../validations/user.validation');
const userController = require('../../controllers/user.controller');

const router = express.Router();

router.post('/users', validate(userValidation.createUser), userController.createUser);
```

## Authentication

Để yêu cầu xác thực cho các tuyến đường nhất định, bạn có thể sử dụng phần mềm trung gian `auth`.

```javascript
const express = require('express');
const auth = require('../../middlewares/auth');
const userController = require('../../controllers/user.controller');

const router = express.Router();

router.post('/users', auth(), userController.createUser);
```

Các tuyến đường này yêu cầu mã thông báo truy cập JWT hợp lệ trong tiêu đề yêu cầu Ủy quyền bằng cách sử dụng Schema Bearer. Nếu yêu cầu không chứa mã thông báo truy cập hợp lệ, lỗi Không được ủy quyền (401) sẽ được đưa ra.

**Tạo Access Tokens**:

An access token can be được tạo thành công bằng cách gọi đến regiser (`POST /v1/auth/register`) hoặc login (`POST /v1/auth/login`) endpoints. Phản hồi của các endpoints cũng chứa refresh tokens (giải thích bên dưới).

Mã thông báo truy cập có hiệu lực trong 30 phút. Bạn có thể sửa đổi thời gian hết hạn này bằng cách thay đổi biến môi trường `JWT_ACCESS_EXPIRATION_MINUTES` trong tệp .env.

**Refreshing Access Tokens**:

Sau khi access token hết hạn, một access token mới có thể được tạo ra, bằng cách gọi đến refresh token endpoint (`POST /v1/auth/refresh-tokens`) và gửi đi một refresh token hợp lệ trong request body. Việc gọi hàm này trả về một access token mới và một refresh token mới.

Mã thông báo làm mới có hiệu lực trong 30 ngày. Bạn có thể sửa đổi thời gian hết hạn này bằng cách thay đổi biến môi trường `JWT_REFRESH_EXPIRATION_DAYS` trong tệp .env.

## Authorization

Phần mềm trung gian `auth` cũng có thể được sử dụng để yêu cầu một số quyền/quyền hạn nhất định để truy cập vào một route.

```javascript
const express = require('express');
const auth = require('../../middlewares/auth');
const userController = require('../../controllers/user.controller');

const router = express.Router();

router.post('/users', auth('manageUsers'), userController.createUser);
```

In the example above, an authenticated user can access this route only if that user has the `manageUsers` permission.

Quyền được phân theo vai trò. Bạn có thể xem quyền/quyền hạn của từng vai trò trong tệp `src/config/roles.js`.

Nếu người dùng thực hiện yêu cầu không có đủ quyền cần thiết để truy cập tuyến đường này, lỗi Cấm (403) sẽ được đưa ra.

## Logging

Import the logger from `src/config/logger.js`. Sử dụng [Winston](https://github.com/winstonjs/winston) logging library.

Logging should be done according to the following severity levels (thứ tự tăng dần từ quan trọng nhất đến ít quan trọng nhất):

```javascript
const logger = require('<path to src>/config/logger');

logger.error('message'); // level 0
logger.warn('message'); // level 1
logger.info('message'); // level 2
logger.http('message'); // level 3
logger.verbose('message'); // level 4
logger.debug('message'); // level 5
```

In development mode, log messages of all severity levels will be printed to the console.

In production mode, only `info`, `warn`, and `error` logs will be printed to the console.\
It is up to the server (or process manager) to actually read them from the console and store them in log files.\
This app uses pm2 in production mode, which is already configured to store the logs in log files.

Note: API request information (request url, response code, timestamp, etc.) are also automatically logged (using [morgan](https://github.com/expressjs/morgan)).

## Custom Mongoose Plugins

The app also contains 2 custom mongoose plugins that you can attach to any mongoose model schema. You can find the plugins in `src/models/plugins`.

```javascript
const mongoose = require('mongoose');
const { toJSON, paginate } = require('./plugins');

const userSchema = mongoose.Schema(
  {
    /* schema definition here */
  },
  { timestamps: true }
);

userSchema.plugin(toJSON);
userSchema.plugin(paginate);

const User = mongoose.model('User', userSchema);
```

### toJSON

The toJSON plugin applies the following changes in the toJSON transform call:

- removes \_\_v, createdAt, updatedAt, and any schema path that has private: true
- replaces \_id with id

### paginate

The paginate plugin adds the `paginate` static method to the mongoose schema.

Adding this plugin to the `User` model schema will allow you to do the following:

```javascript
const queryUsers = async (filter, options) => {
  const users = await User.paginate(filter, options);
  return users;
};
```

The `filter` param is a regular mongo filter.

The `options` param can have the following (optional) fields:

```javascript
const options = {
  sortBy: 'name:desc', // sort order
  limit: 5, // maximum results per page
  page: 2, // page number
};
```

The plugin also supports sorting by multiple criteria (separated by a comma): `sortBy: name:desc,role:asc`

The `paginate` method returns a Promise, which fulfills with an object having the following properties:

```json
{
  "results": [],
  "page": 2,
  "limit": 5,
  "totalPages": 10,
  "totalResults": 48
}
```

## Linting

Linting is done using [ESLint](https://eslint.org/) and [Prettier](https://prettier.io).

In this app, ESLint is configured to follow the [Airbnb JavaScript style guide](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb-base) with some modifications. It also extends [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier) to turn off all rules that are unnecessary or might conflict with Prettier.

To modify the ESLint configuration, update the `.eslintrc.json` file. To modify the Prettier configuration, update the `.prettierrc.json` file.

To prevent a certain file or directory from being linted, add it to `.eslintignore` and `.prettierignore`.

To maintain a consistent coding style across different IDEs, the project contains `.editorconfig`

## Contributing

Contributions are more than welcome! Please check out the [contributing guide](CONTRIBUTING.md).

## Inspirations

- [danielfsousa/express-rest-es2017-boilerplate](https://github.com/danielfsousa/express-rest-es2017-boilerplate)
- [madhums/node-express-mongoose](https://github.com/madhums/node-express-mongoose)
- [kunalkapadia/express-mongoose-es6-rest-api](https://github.com/kunalkapadia/express-mongoose-es6-rest-api)

## License

[MIT](LICENSE)
