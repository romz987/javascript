# Паттерны проектирования
В контексте React JS



----  
## Порождающие паттерны    
Создание компонентов    


1. Factory pattern (Фабричный метод)    
Используется в React для динамического создания компонентов. Например, можно создавать разные компоненты на основе пропсов.    

```javascript
const Button = ({ type, children }) => {
    if (type === 'primary') return <button className="btn-primary">{children}</button>;
    if (type === 'secondary') return <button className="btn-secondary">{children}</button>;
    return <button>{children}</button>;
};  
```  



2. Higher-Order Component (HOC) (Фабричный метод)    
Позволяет создавать новые компоненты, добавляя к ним дополнительный функционал.     
!!! Не очень понятно, что это такое. Пример не репрезентативен !!!    



3. Singleton (Одиночка)  
Используется, например, в Context API для хранения состояния приложения.  



----  
## Структурные паттерны    
Помогают организовать компоненты и управлять их взаимодействием.   


1. Container-Presenter (Контейнер и представление)  
Разделяет логику и представление, что делает код более читаемым и поддерживаемым.  

```javascript
// Контейнер
const UserContainer = () => {
    const [user, setUser] = useState({ name: 'Irina' });
    return <UserPresenter user={user} />;
};  
  
// Представление
const UserPresenter = ({ user }) => <h1>{user.name}</h1>;
```  



2. Composite (Компоновщик)  
Позволяет строить сложные компоненты из более мелких.  

```javascript 
const Card = ({ children }) => <div className="card">{children}</div>;

const App = () => (
    <Card>
        <h2>Title</h2>
        <p>Description</p>
    </Card>
);
```  



3. Decorator   
Похож на HOC, но добавляет поведение к существующим компонентам.  

```javascript 
const withBorder = (Component) => (props) => (
    <div style={{ border: '1px solid black' }}>
        <Component {...props} />
    </div>
);

const BorderedComponent = withBorder(MyComponent);
```



----
## Поведенческие паттерны  
Они отвечают за управление состоянием, взаимодействие между компонентами и обработку событий.  


1. Observer (Наблюдатель)   
Реализован через Context API или Redux, когда подписчики реагируют на изменения состояния.  

```javascript 
const ThemeContext = React.createContext();

const App = () => {
    const [theme, setTheme] = useState('light');
    return (
        <ThemeContext.Provider value={{ theme, setTheme }}>
            <ChildComponent />
        </ThemeContext.Provider>
    );
};

const ChildComponent = () => {
    const { theme } = useContext(ThemeContext);
    return <p>Current theme: {theme}</p>;
};
```  



2. State Pattern (Состояние)  
Используется в Redux и useReducer, где состояние приложения изменяется через диспатч.  

```javascript 
const reducer = (state, action) => {
    switch (action.type) {
        case 'increment':
            return { count: state.count + 1 };
        default:
            return state;
    }
};

const Counter = () => {
    const [state, dispatch] = useReducer(reducer, { count: 0 });

    return (
        <div>
            <p>{state.count}</p>
            <button onClick={() => dispatch({ type: 'increment' })}>+</button>
        </div>
    );
};
```
  


3. Strategy (Стратегия)  
Позволяет переключать алгоритмы, например, разные способы сортировки.  


```javascript
const strategies = {
    asc: (a, b) => a - b,
    desc: (a, b) => b - a,
};

const SortList = ({ items, strategy }) => {
    const sorted = [...items].sort(strategies[strategy]);
    return <ul>{sorted.map((item) => <li key={item}>{item}</li>)}</ul>;
};
```



4. Command (Команда)  
Используется в Redux Middleware, где действия (actions) передаются в store.  



5. Mediator (Посредник)  
Используется в React Context API или Redux для координации взаимодействия компонентов.  
