# redux-json-api-handlers

Initial commit. Readme and usage guide will be added later

## Api methods

### `createLoadHandler(resourceType: string, options: object): nextState`
Use it for handle success data loading

Options: 
```js
const options = {
  mapToKey: bool|string,  // default: false, map result to custom reducer key
  withLoading: bool,      // default: true, enable/disable loading params
  idsOnly: bool           // default: false, map entities ids to array
}
```

#### Simple example
Initial state looks like: 
```js
state = {
  posts: {
    isLoaded: false,
    isLoading: false,
    posts: {}
  }
}
```
```js
const handlers = {
  [LOAD_POSTS.SUCCESS]: createLoadHandler('posts')
}
```
Resulted state looks like: 
```js
state = {
  posts: {
    isLoaded: true,
    isLoading: false,
    posts: {
      '1': {
        id: 1,
      }
    }
  }
}
```

#### Custom example
Initial state looks like: 
```js
state = {
  posts: {
    isLoadedPostIds: false,
    isLoadingPostIds: false,
    postIds: []
  }
}
```
Handler:
```js
const handlers = {
  [LOAD_POSTS.SUCCESS]: createLoadHandler('posts', { mapToKey: 'postIds', idsOnly: true })
}
```
Resulted state looks like: 
```js
state = {
  posts: {
    isLoadedPostIds: true,
    isLoadingPostIds: false,
    postIds: ['1']
  }
}
```


### `createDeleteHandler(stateKey: string): nextState`
Use it for handle delete data.

Action payload should have `deletedId` param

#### Simple example
Initial state looks like: 
```js
state = {
  posts: {
    posts: {
      '1': {
        id: 1,
      },
      '2': {
        id: 2,
      }
    }
  }
}
```
Handler:
```js
const handlers = {
  [DELETE_POST.SUCCESS]: createDeleteHandler('posts')
}
```
Resulted state looks like: 
```js
state = {
  posts: {
    posts: {
      '2': {
        id: 2,
      }
    }
  }
}
```

#### Custom example
Initial state looks like: 
```js
state = {
  posts: {
    postIds: ['1', '2']
  }
}
```
```js
const handlers = {
  [DELETE_POST.SUCCESS]: createDeleteHandler('postIds')
}
```
Resulted state looks like: 
```js
state = {
  posts: {
    postIds: ['1']
  }
}
```
