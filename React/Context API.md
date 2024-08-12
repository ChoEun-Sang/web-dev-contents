# Context API

일반적인 React 애플리케이션에서 데이터는 위에서 아래로 (즉, 부모로부터 자식에게) props를 통해 전달합니다. 애플리케이션 안의 여러 컴포넌트들에 전해줘야 하는 props의 경우, 중간 컴포넌트에 불필요한 프로퍼티 전달하는 Prop drilling이 발생할 수 있습니다.

context를 이용하면 단계마다 일일이 props를 넘겨주지 않고도 컴포넌트 트리 전체에 데이터를 제공할 수 있습니다.

## API

- React.createContext

```js
const MyContext = React.createContext(defaultValue);
```

Context 객체를 만든다. Context 객체를 구독하고 있는 컴포넌트를 렌더링할 때 React는 트리 상위에서 가장 가까이 있는 짝이 맞는 Provider로부터 현재값을 읽습니다.

defaultValue 매개변수는 트리 안에서 적절한 Provider를 찾지 못했을 때만 쓰이는 값입니다.

- Context.Provider
  <MyContext.Provider value={/_ 어떤 값 _/}>
  Provider 컴포넌트는 value prop을 받아서 이 값을 하위에 있는 컴포넌트에게 전달합니다. Provider 하위에서 context를 구독하는 모든 컴포넌트는 Provider의 value prop가 바뀔 때마다 다시 렌더링 됩니다.

- Class.contextType

- Context.Consumer

```js
<MyContext.Consumer>
  {(value) => /_ context 값을 이용한 렌더링 _/}
</MyContext.Consumer>
```

이 컴포넌트를 사용하면 함수 컴포넌트안에서 context를 구독할 수 있습니다.

Context.Consumer의 자식은 함수여야합니다. 이 함수는 context의 현재값을 받고 React 노드를 반환합니다. 이 함수가 받는 value 매개변수 값은 해당 context의 Provider 중 상위 트리에서 가장 가까운 Provider의 value prop과 동일합니다. 상위에 Provider가 없다면 value 매개변수 값은 createContext()에 보냈던 defaultValue와 동일할 것입니다.

```js
Context.displayName
const MyContext = React.createContext(/_ some value _/);
MyContext.displayName = 'MyDisplayName';

<MyContext.Provider> // "MyDisplayName.Provider" in DevTools
<MyContext.Consumer> // "MyDisplayName.Consumer" in DevTools

```

React 개발자 도구는 이 문자열을 사용해서 context를 어떻게 보여줄 지 결정합니다.

언제 context를 써야 할까
context는 React 컴포넌트 트리 안에서 전역적(global)이라고 볼 수 있는 데이터를 공유할 수 있도록 고안된 방법입니다. 예를 들면, 현재 로그인한 유저, 테마, 선호하는 언어 등이 있습니다.

```js
const ThemeContext = React.createContext("light");

class App extends React.Component {
  render() {
    // Provider를 이용해 하위 트리에 테마 값을 보내줍니다.
    // 아무리 깊숙히 있어도, 모든 컴포넌트가 이 값을 읽을 수 있습니다.
    // 아래 예시에서는 dark를 현재 선택된 테마 값으로 보내고 있습니다.
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}
// 이젠 중간에 있는 컴포넌트가 일일이 테마를 넘겨줄 필요가 없습니다.

function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  // 현재 선택된 테마 값을 읽기 위해 contextType을 지정합니다.
  // React는 가장 가까이 있는 테마 Provider를 찾아 그 값을 사용할 것입니다.
  // 이 예시에서 현재 선택된 테마는 dark입니다.
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;
  }
}
```

- 주의사항
  Provider의 부모가 렌더링 될 때마다 불필요하게 하위 컴포넌트가 다시 렌더링 되는 문제가 생길 수도 있습니다.

## 참고

[Context API](https://ko.legacy.reactjs.org/docs/context.html#when-to-use-context)
