# object-optimizer

```javascript
const isObject = obj => obj && typeof obj === 'object';
const hasKey = (obj, key) => key in obj;

function optimizer(obj) {
  return new Proxy(obj, {
    get: function(target, name) {
      return hasKey(target, name) ?
        (isObject(target[name]) ? safe(target[name]) : target[name]) : undefined;
    },
    set: function(target, key, value, receiver) {
      console.trace();
      console.log(`################### set ${key}! ${target[key]} replace by ${value} ###################`);
      target[key] = value;
      return true;
    }
  });
}

optimizer(myObj);
```
