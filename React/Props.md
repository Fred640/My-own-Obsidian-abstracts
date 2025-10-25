Props - аргументы, араметры которые компонент может принимать из вне, но обмен всезда пнросиходит от родителя к дочернему компоненту. Обратный процусс можно реализовать с помощью функции обратного вызова 

Простой пример передачи props
```
function App() {

  return (
    <div className="App">
      <PostItem post={{title: "Javascript", id: 1, body: "description"}}/>
      <PostItem post={{title: "Javascript", id: 2, body: "description"}}/>
      <PostItem post={{title: "Javascript", id: 3, body: "description"}}/>
    </div>
  );
}
```

```
const PostItem = (props) => {

    return(
    <div className="post">
        <div className="post__content">
            <h5>{props.post.id} {props.post.title}</h5>
            <div>
                {props.post.body}
            </div>
        </div>
        <button>Удалить</button>
    </div>
    )
}
```

![[Pasted image 20250913115613.png]]

Также можно реализовать такой метод передачи props
```
function App() {

  const [posts, setPosts] = useState([
    {title: "Javascript", id: 1, body: "description"},
    {title: "Javascript", id: 2, body: "description"},
    {title: "Javascript", id: 3, body: "description"},
  ])

  return (
    <div className="App">
      {posts.map(post => <PostItem post={post}/>)}
    </div>
  );
}
```

!!! Но когда создаеться список обязательным условием являеться определение ключа, этот ключ должен всегда быть **статичным** и **уникальным**.  Ключи позволяют реакту оптимизировать рендеринг - отрисовывать не весь список а только те элементы в которых произошли изменения

поэтому

```
return (
    <div className="App">
      {posts.map(post => <PostItem post={post} key={post.id}/>)}
    </div>
  );
```

[[Props children]]