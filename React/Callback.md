Это функция обратного вызова которая может передовать props от дочернего компонента к родительскому

пример передачи информации о посте из формы вверх к App компоненту через callback функцию

```
function App() {

  const [posts, setPosts] = useState([
    {title: "Javascript", id: 1, body: "description"},
    {title: "Javascript", id: 2, body: "description"},
    {title: "Javascript", id: 3, body: "description"},
  ])


  const createPost = (newPost) => {
    setPosts([...posts, newPost])
  }


  return (
    <div className="App">
      <PostForm create={createPost}/>
    </div>
  );
}
```

```
const PostForm = ({create}) => {
    
    const [post, setPost] = useState({title:"", body:""})
    

  const addPost = (event) => {
    event.preventDefault()
    const newPost = {...post, id: Date.now()}
    create(newPost)
    setPost({title:"", body:""})
  }

    return(
      <form>
        <Inp 
        value={post.title}
        placeholder="Title"
        onChange={event => setPost({...post, title: event.target.value})}
        />
        <Inp 
        value={post.body}
        placeholder="Description"
        onChange={event => setPost({...post, body: event.target.value})}
        />
        <Btn style={{marginTop: "5px"}} onClick={addPost}>Add Post</Btn>
      </form>
    )
}
```

