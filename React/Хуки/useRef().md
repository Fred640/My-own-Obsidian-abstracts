С помощью этого хука мы можем получить доступ к DOM элементу 


```
function App() {

  const [post, setPost] = useState([
    {id:1, title:"javascript", body:"Javascript - Язык програмирования"},
    {id:2, title:"javascript", body:"Javascript - Язык програмирования"},
    {id:3, title:"javascript", body:"Javascript - Язык програмирования"},
  ])

  const [title, setTitle] = useState()
  const bodyInputRef = useRef()
  const addNewPost = (event) => {
    event.preventDefault()
    console.log(title)
    console.log(bodyInputRef.current.value)

  }

  return (
    <div className="App">
      <form>
        {/* Управляемый компонент */}
      <MyInput 
        type="text" 
        placeholder="Название поста"

        value={title}
        onChange={e => setTitle(e.target.value)}
      />
      {/* Неуправляемый компонент */}
      <MyInput 
      ref={bodyInputRef}
      type="text" 
      placeholder="Описание поста"/>
      <MyButton onClick={addNewPost} disbled>lsidjgfos</MyButton>
      </form>
      <PostList post = {post}/>

    </div>
    
  );
}
```

```
const MyInput = React.forwardRef((props, ref) => {
    return(
        <input {...props} className={classes.myInput} ref={ref} />
    )
})
```