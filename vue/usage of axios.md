# Axios 공통

### ex1

```javascript
import axios
import router from '../router'

const DOMAIN = 'http://localhost:3000'
const UNAUTHORIZED = 401
const onUnauthorized = ()=>{
    router.push(`/login?rPath=${encodeURIComponent(location.pathname)}`)
}

const request = (method, url, data) =>{

    return axios({
        method,
        url:DOMAIN+url,
        data
    }).then(result=>result.data)
    .catch(result => {
        const {status} = result.response

        if (status=== UNAUTHORIZED){
            onUnauthorized()
        }
        throw result.response
    })
}

export const setAuthInHeader = token =>{
    axios.defaults.headers.common['Authorization'] = token? `Bearer ${token}`:null
}
```

```javascript
request("get", "/login", payload);
```

### ex2

```javascript
import axios from 'axios'

const $http = axios.create({
    baseURL : (function(){
        return commonTutils.CONSTANT.URL
    })(),
    header:{
        'Access-Control-Allow-Origin':'*',
        'Content-type':'applicaton/json;charset=UTF-8'
    },
    node:'no-cors'
});

$http.all = axios.all;
$http.spread = axios.spread;
$http.interceptors.reqeust.use(
    (config)=>{
       ...
    },
    (error)=>{
        ...
    }
)

$http.interceptors.response.use(
    (response)=>{
        ...
        return response
    },
    (error)=>{
        ...
        return Promise.reject(error)
    }
)
```

```javascript
$http.post("/login", {});
```
