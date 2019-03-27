## 随着流行框架的兴起，Axios、Request、Superagent、Fetch、Supertest等http库也各有千秋。[优缺点](http://www.mamicode.com/info-detail-2558633.html)  
create by Chanphy on 2019.3.27
### axios的简单封装  

```javascript
  import axios from 'axios';
  let qs = require('qs');
  
  let instance = axios.create({
    baseURL: 'https://some-domain.com/api/' // get other options visit https://www.npmjs.com/package/axios
  });
  
  // Add a request interceptor
  instance.interceptors.request.use(function (config) {
    // Do something before request is sent
    return config;
  }, function (error) {
    // Do something with request error
    return Promise.reject(error);
  });
 
  // Add a response interceptor
  instance.interceptors.response.use(function (response) {
    // Do something with response data
    return response;
  }, function (error) {
    // Do something with response error
    return Promise.reject(error);
  });
  
  export function post(url, params = {}) {
    return new Promise((resolve, reject) => {
      instance.post(url, qs.stringify(params))
      .then(res => {
        resolve(res);
      })
      .catch(err => {
        reject(err);
      });
    });
  }
  
  export function get(url, params = {}) {
    return new Promise((resolve, reject) => {
      instance.get(url, { params })
      .then(res => {
        resolve(res);
      })
      .catch(err => {
        reject(err);
      });
    });
  }
  
```   

