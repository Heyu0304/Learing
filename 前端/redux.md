# Redux初入门
废话不多说，关于redux组成，由这几个action,reducer,store基本的来组成的。  
action:

        const ADD_TODO = 'ADD_TODO';
        function addTodo(text) {
          return {
              type: ADD_TODO,
              text
            }
          }

reducer:  

    function todoApp(state = initialState, action) {
      switch (action.type) {
        case SET_VISIBILITY_FILTER:
            return Object.assign({}, state, {
              visibilityFilter: action.filter
                })
        default:
          return state
        }
    }
这里要记一下，不能直接动state。这里用的是es6语法，可以在参数里面直接初始化state

store:   

    import { createStore } from 'redux'
    let todoApp = combineReducers({
        todos,
        visibleTodoFilter
      }
    let store = createStore(todoApp)
store个人感觉是一个对象，如果想上边那样,用es6语法的化，store就是这样  

      store={
        todos: ...,
        visibilityFilter: ....,
      }

结合React的化，需要这三个方法,mapStateToProps,mapDispatchToProps,connect()的方法。Redux关键的难点在于设计store和异步调用，effects方面上更新store。如果更加的复杂，比如打印日志，则要使用中间件middleware来使用。后续再更新。
